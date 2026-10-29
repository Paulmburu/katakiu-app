# KataKiu customer app: agent instructions

> **Repository status:** planning documents only, prepared 29 October 2026. No Flutter project exists yet. Phase F0 in [DELIVERY_PLAN.md](DELIVERY_PLAN.md) creates it.

This file applies to the whole `katakiu-app` repository unless a more specific instruction file overrides it. **User directions take precedence** over these conventions. If a direction conflicts with a backend business invariant, explain the conflict and record the decision; never silently weaken the purchase proof.

## MVP first: keep it simple

This is an MVP. Build the simplest version that works and that a new developer can follow in one read.

- **State and wiring.** Use Riverpod with handwritten providers, Dart 3 sealed classes and manual `fromJson`. Do not use code generation (Freezed, json_serializable, riverpod_generator) until its benefit is clear and agreed.
- **No speculative abstractions.** Add an interface only when a second implementation exists or a test needs a fake. Do not add generic base classes, plugin systems or a second HTTP client.
- **Fewer screens, fully working.** Build only against **live** endpoints. A planned feature stays hidden behind its documented fallback.
- **Simple never means weaker.** The backend's business invariants still hold (§3).

### Task files to update when work completes

Update these in the same change as the code. A task is not done until its tracker says so, with evidence.

| File | Update |
|---|---|
| [DELIVERY_PLAN.md](DELIVERY_PLAN.md) | Tick `- [x] Fn-Tm`; update the progress count in the header and the phase status |
| [PROGRESS.md](PROGRESS.md) | Session entry: tasks, flavour, commands run with results, device runs, open issues, next action |
| [ROADMAP.md](ROADMAP.md) | Gate checkboxes (AG1–AG3) when all of a gate's evidence exists; the change log for schedule changes |
| [ARCHITECTURE_PLAN.md](ARCHITECTURE_PLAN.md) | Only when a design decision changes (structure, flows, packages, endpoints used) |
| [PRD.md](PRD.md) | Only when an app requirement (AR-xx) changes |

## 1. Sources to read first

Before changing anything, read the relevant parts of:
0. **[README.md](README.md):** the order of implementation and the per-task loop.
1. **[PRD.md](PRD.md):** the requirement (AR-xx) you are implementing and its source FR.
2. **[ARCHITECTURE_PLAN.md](ARCHITECTURE_PLAN.md):**
   - layers (§1–§3);
   - flavours (§3.2);
   - the screen and widgets (§5);
   - endpoint consumption (§6.0);
   - errors (§8);
   - security (§9).
3. **[DELIVERY_PLAN.md](DELIVERY_PLAN.md):** the task's ID and its done criterion.
4. **The backend API reference:**
   - [customer-app.md](../katakiu-backend/docs/api/reference/customer-app.md);
   - [authentication.md](../katakiu-backend/docs/api/reference/authentication.md);
   - [conventions.md](../katakiu-backend/docs/api/reference/conventions.md);
   - [errors.md](../katakiu-backend/docs/api/reference/errors.md).

   These are captured from real traffic, so use their payloads as DTO test fixtures.
5. **The design** for the screen: `katakiu_mobile_ui_production/<batch>/screen.png` and `code.html`, plus [DESIGN.md](katakiu_mobile_ui_production/mobile_loyalty_verification/DESIGN.md). If you cannot view images, use the batch's `code.html`: it has the same screen as markup, including texts, states and colours.

For business rules, the backend [PRD](../katakiu-backend/PRD.md) and [AGENTS](../katakiu-backend/AGENTS.md) are authoritative.

## 2. Stack and structure

- **Stack:** Flutter (Android and iOS), `flutter_riverpod`, `http` as the **only** HTTP client (wrapped by `ApiClient`), `go_router` and `flutter_secure_storage`. Other packages are added only in the phase listed in ARCHITECTURE_PLAN §11.
- **Feature-based DDD:** `features/<feature>/{domain,application,infrastructure,presentation}`, with the dependency direction from ARCHITECTURE_PLAN §1:
  - **domain** imports nothing from Flutter, Riverpod, `http` or Firebase;
  - **infrastructure** maps DTOs to domain types, and DTOs never reach presentation;
  - **providers** compose dependencies, and widgets never construct repositories or call `ApiClient`.
- **One folder per screen:**
  - `presentation/<screen>/<screen>_screen.dart`, plus the controller if it has one;
  - `widgets/` for widgets used only by that screen.
- **Promotion rule:**
  - a widget shared within a feature moves to `features/<f>/presentation/widgets/`;
  - a widget shared across features moves to `core/ui/`.
  - Never move a widget up "in case".
- **`core/`** holds only code shared by two or more features: network, security, observability and ui.
- **Styling** goes only through the `lib/core/theme` tokens (`KkColors`, `KkText`, `KkSpace`, `KkRadius`, `KkSize`, `KkStatusColors`) and `KkTheme.light()` (ARCHITECTURE_PLAN §10). Never use raw hex colours, font sizes, paddings or radii in widgets; `test/theme/no_raw_styles_test.dart` must pass. Use `tealText` and `coralText` for text, not `teal` or `coral` (contrast, §10.7).
- **Points** are `BigInt` values parsed from the API's decimal strings. Never use `double`. Timestamps stay UTC in the domain and are formatted locally in presentation.

## 3. Client-side invariants

These are the app's share of the backend [business invariants](../katakiu-backend/AGENTS.md#3-business-invariants):
1. **The app never computes or awards points.** Show "expected" points before confirmation; only server-confirmed values count (backend invariants 1 and 10).
2. **The scanner reads QR codes only** (`BarcodeFormat.qrCode`). Retail barcodes must never be submitted (backend FR-05).
3. **Product codes and pass credentials live in memory only.** Never persist, log, send to analytics or put them in a URL. Drop the raw code once CL-01 returns (backend invariant 13).
4. **One request in flight per mutation,** with an `Idempotency-Key` per logical attempt that is **reused on retry** (backend invariant 3).
5. **A timeout is an unknown outcome.** Resolve it by a same-key replay or a status check, never by repeating the action as new. Offline, never finalise anything (backend invariant 9).
6. **Logout and session loss clear all account-scoped state,** including the secure store and providers.
7. **Never show placeholder business data.** A field the server doesn't return is hidden, not faked.

## 4. API consumption rules

- **All calls go through `ApiClient`.** It handles the envelope, the bearer token, the single-flight refresh, `X-Request-ID`, idempotency and timeouts.
- **Map every error code** the endpoint can return (ARCHITECTURE_PLAN §8 and the backend `errors.md`). Show safe messages, never raw server text.
- **Build only against live endpoints** (ARCHITECTURE_PLAN §16.1). Never build a screen on a planned endpoint with mock data and present it as done.
- **New endpoint needs go to the backend first.** Record the need in ARCHITECTURE_PLAN §16.3; it must be agreed and added to the backend catalogue before any app work depends on it.
- **API drift.** If the backend API changes after you start:
  1. regenerate the reference (`make api-docs` in katakiu-backend);
  2. update the affected DTO fixtures and tests;
  3. record the new backend commit in PROGRESS.md;
  4. update ARCHITECTURE_PLAN §6.0 and §16 if endpoints were added or changed.
- **Trust the server, not the client.** Never trust client-side eligibility, role or point values.

## 5. Flavours

- **Two flavours:** `dev` and `prod` (ARCHITECTURE_PLAN §3.2). Always pass both `--flavor <x>` and `--dart-define-from-file=config/<x>.json`.
- **Development** always uses **dev**, against a local or seeded backend. Never use the test OTP or seeded test accounts against prod.
- **Flavour checks** live only in `app/config.dart` and the providers. Domain and application code never branch on the flavour.
- **Secrets** never go in `config/*.json`. CI injects them. Your LAN IP goes in a git-ignored `config/dev.local.json`.

## 6. Commands

| Action | Command | Prerequisite |
|---|---|---|
| Install dependencies | `flutter pub get` | Flutter SDK (version recorded in PROGRESS.md) |
| Format check | `dart format --set-exit-if-changed .` | Run `dart format .` to fix |
| Static analysis | `flutter analyze` | Dependencies installed |
| Unit and widget tests | `flutter test` | No backend needed |
| Integration journey | `flutter test integration_test --flavor dev --dart-define-from-file=config/dev.json` | Local seeded backend running (`make seed` in katakiu-backend); emulator or device |
| Run dev | `flutter run --flavor dev --dart-define-from-file=config/dev.json` | Local backend; use `config/dev.local.json` on a physical device |
| Run prod | `flutter run --flavor prod --dart-define-from-file=config/prod.json --release` | Prod backend reachable; **only when authorised** |
| Release builds | See the command table in ARCHITECTURE_PLAN §3.2 | Signing configured; never commit keys |

Do not print environment files, signing files or secrets. If a check cannot run, report the exact limitation and do not tick the task.

## 7. Verification expectations

- **Unit tests:** domain types and use cases, with fake repositories.
- **DTO tests:** for every repository method, using the **captured payloads** from the backend API reference.
- **Controller tests:** with `ProviderContainer` overrides.
- **Widget tests:** every screen state listed in ARCHITECTURE_PLAN §5.1, and every `core/ui` component variant.
- **Integration:** the journey on the dev flavour against the seeded backend (F4-T08).
- **Physical devices:** for scanning, the pass and secure storage (F3-T15/16). Emulators are not enough.
- **Before claiming a task done,** run format, analyze and the relevant tests, plus the full test suite once at the end of a phase.

## 8. Security and operations

- **Sensitive values never leave memory.** No token, OTP, product code, pass credential or phone number in logs, analytics, crash reports, committed screenshots, test fixtures with real data, or PROGRESS.md.
- **Never commit signing material:** keystores, provisioning profiles, `key.properties`, Firebase service accounts or store credentials.
- **Ask before outward-facing actions.** Do not publish to stores, upload builds, change Firebase, Sentry or PostHog projects, send push notifications, or point a build at production unless the current task authorises it.
- **Never ship a test bypass.** No test OTP, debug token or mock repository may be reachable in a release build.

## 9. Scope and documentation discipline

- **Designs:** follow them, but treat illustrated names, balances and codes as fixtures.
- **Not built:** conditional extensions (PRD §3) and mockup-only features. Planned features stay hidden with their fallback (ARCHITECTURE_PLAN §16.2).
- **When a requirement changes,** update PRD, ARCHITECTURE_PLAN and DELIVERY_PLAN together. If a business rule is affected, the backend PRD changes first.
- **Do not decide open questions yourself:** neither the app questions (DELIVERY_PLAN §6, Q1–Q9) nor business decisions (backend D-01–D-08). Use the documented default or fallback, mark the item as waiting on the owner, and continue with unblocked tasks.
- **Final reports** state what changed, what was actually checked (commands, devices, flavour) and any remaining limitation. Never claim tests, device runs or releases that did not happen.

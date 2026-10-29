# KataKiu customer app: progress and evidence log

> **Current phase:** none (F0 not started) · **Tasks done:** 0 / 109 · **Last updated:** 2026-10-29
> **Tasks:** [DELIVERY_PLAN.md](DELIVERY_PLAN.md) · **Gates:** [ROADMAP.md §4](ROADMAP.md#4-gates) · **Design:** [ARCHITECTURE_PLAN.md](ARCHITECTURE_PLAN.md) · **Rules:** [AGENTS.md](AGENTS.md)

**Resume here:** next task **F0-T01**. Backend dependency: `katakiu-backend` branch `feat/seed-endpoint-tests-api-docs` (PR #2), or `develop` once PR #2 is merged. Update this line at the end of every session.

**What goes here.** Record the evidence for every ticked task: commands run with their results, device runs and open issues. Never record tokens, OTPs, product codes or credentials (see ARCHITECTURE_PLAN §9).

## Environment

Filled in at F0-T04 and updated when versions change.

| Item | Value |
|---|---|
| Flutter / Dart | — |
| Android min SDK / iOS minimum | — (Q1) |
| Backend commit tested against | — |
| App ID: dev / prod | `com.katakiu.app.dev` / `com.katakiu.app` (proposed, Q8) |
| Config file: dev / prod | `config/dev.json` / `config/prod.json` (+ git-ignored `config/dev.local.json`) |
| `appFlavor` available in SDK | — (confirm at F0-T08d) |
| Pinned packages | — |

## Device matrix

Filled in from F1 onward.

| Device | OS | Flavour | Sign-in | Scan (QR) | Pass readable by merchant | Notes |
|---|---|---|---|---|---|---|
| — | — | — | — | — | — | — |

## Session log

Newest entry first. Copy this template for each work session:

```markdown
### YYYY-MM-DD — <phase> — <short title>
**Tasks:** F0-T01, F0-T02
**Flavour:** dev | prod
**Changed:** <files / screens>
**Commands and results:**
- `flutter analyze` → 0 issues
- `flutter test` → N passed
- device run: <device> → <result>
**Open issues:** <none | description + task/blocker ID>
**Next action:** <task ID>
```

No sessions yet.

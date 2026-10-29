---
name: Mobile Loyalty & Verification
colors:
  surface: '#f6faff'
  surface-dim: '#cedce7'
  surface-bright: '#f6faff'
  surface-container-lowest: '#ffffff'
  surface-container-low: '#eaf5ff'
  surface-container: '#e2f0fb'
  surface-container-high: '#dceaf5'
  surface-container-highest: '#d7e4f0'
  on-surface: '#101d25'
  on-surface-variant: '#3c4946'
  inverse-surface: '#25323b'
  inverse-on-surface: '#e5f2fe'
  outline: '#6c7a76'
  outline-variant: '#bbcac5'
  surface-tint: '#006b5f'
  primary: '#006b5f'
  on-primary: '#ffffff'
  primary-container: '#0db3a0'
  on-primary-container: '#003e37'
  inverse-primary: '#52dbc7'
  secondary: '#835500'
  on-secondary: '#ffffff'
  secondary-container: '#ffb548'
  on-secondary-container: '#704800'
  tertiary: '#51606f'
  on-tertiary: '#ffffff'
  tertiary-container: '#92a1b2'
  on-tertiary-container: '#293846'
  error: '#ba1a1a'
  on-error: '#ffffff'
  error-container: '#ffdad6'
  on-error-container: '#93000a'
  primary-fixed: '#73f8e3'
  primary-fixed-dim: '#52dbc7'
  on-primary-fixed: '#00201c'
  on-primary-fixed-variant: '#005047'
  secondary-fixed: '#ffddb4'
  secondary-fixed-dim: '#ffb955'
  on-secondary-fixed: '#291800'
  on-secondary-fixed-variant: '#633f00'
  tertiary-fixed: '#d4e4f7'
  tertiary-fixed-dim: '#b8c8da'
  on-tertiary-fixed: '#0d1d2a'
  on-tertiary-fixed-variant: '#394857'
  background: '#f6faff'
  on-background: '#101d25'
  surface-variant: '#d7e4f0'
typography:
  headline-lg:
    fontFamily: Inter
    fontSize: 22px
    fontWeight: '700'
    lineHeight: 28px
  title-md:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '600'
    lineHeight: 22px
  title-sm:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '500'
    lineHeight: 20px
  label-lg:
    fontFamily: Inter
    fontSize: 13px
    fontWeight: '600'
    lineHeight: 18px
  label-md:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '500'
    lineHeight: 16px
  label-sm:
    fontFamily: Inter
    fontSize: 11px
    fontWeight: '500'
    lineHeight: 14px
  body-md:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '400'
    lineHeight: 18px
  body-sm:
    fontFamily: Inter
    fontSize: 11px
    fontWeight: '400'
    lineHeight: 16px
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  gutter: 16px
  margin: 16px
  space-xs: 4px
  space-sm: 8px
  space-md: 12px
  space-lg: 16px
  space-xl: 24px
---

## Brand & Style
This design system defines a high-trust, mobile-first utility designed for verified purchases and consumer rewards. Built to perform reliably under varied ambient lighting and network constraints across Kenya, it avoids ornamental noise, skeuomorphism, and heavy effects in favor of functional clarity.

### Personality & Tone
- **Direct & Functional:** Clear transactional flows focused on scanning, verification, and balance updates.
- **Trustworthy & Crisp:** High text-to-background contrast with distinct state signifiers (confirmation, pending, error).
- **Tactile Utility:** Strict flat surfaces paired with structured 1px structural dividing lines.

### Design Movement
**Modern Functional Flat:** Zero gradients, zero glassmorphism, zero neon glows. Visual depth is established purely through surface-color hierarchy (#FFFFFF base against #F5F7F8 neutral containers) and hairline structural borders.

## Colors
The palette uses distinct color assignments to prevent cognitive friction during rapid retail and checkout scanning.

### Semantic Mapping
- **Teal (`#0DB3A0`):** Primary brand action color. Applied to filled action buttons, confirmed transaction badges, active tab navigation, and interactive text links.
- **Amber (`#FFB547`):** High-salience scanner focus bracket color, primary scan trigger indicators, pending/under-review points, and temporal notices.
- **Midnight (`#071724`):** Primary typography, headings, structural emphasis, and high-contrast summary cards (e.g., active loyalty card or tier overview).
- **Aqua (`#7AE1D6`):** Supporting surface tone. Used for light tint fills behind pending statuses, point progress tracks, and secondary informative chips.
- **Coral (`#EF6A6A`):** Critical state tone. Applied to rejected/failed scans, reversed points, expired reward vouchers, destructive actions, and age-gate warnings.
- **White (`#FFFFFF`):** Primary viewport background, card surfaces, top navigation bars, and bottom navigation container.
- **Soft Neutral Surface (`#F5F7F8`):** Off-white base for screen canvases, input field resting states, and secondary card containers.
- **Divider (`#E6EAED`):** Hairline borders, structural card outlines, and item separators.
- **Secondary Text (`#66737D`):** Subtext, receipt timestamps, merchant addresses, helper captions, and unselected icons.

## Typography
Typographic hierarchy is restricted to a single typeface family (`Inter`) to ensure predictable cross-platform rendering and compact density on handheld screens.

### Hierarchy & Assignments
- **Main Numerical Value (`22px / 700 / lineHeight: 28px`):** Used exclusively for total reward balances, scan count totals, and key numeric currency displays.
- **Section Heading (`16px / 600 / lineHeight: 22px`):** Section titles, module headers, and bottom-sheet titles.
- **App-Bar Title (`14px / 500 / lineHeight: 20px`):** Top app-bar headers and centered viewport navigation titles.
- **Primary Action Label (`13px / 600 / lineHeight: 18px`):** Primary and secondary touch target button labels.
- **Body Text (`12px / 400 / lineHeight: 18px`):** General description text, transaction detail rows, and policy paragraphs.
- **Bottom-Navigation Label (`12px / 500 / lineHeight: 16px`):** Tab bar item descriptions.
- **Status Label & Chip (`11px / 500 / lineHeight: 14px`):** Verification status pills, tier labels, and inline tag components.
- **Metadata & Helper (`11px / 400 / lineHeight: 16px`):** Helper text, field validation captions, timestamps, and receipt reference numbers.

## Layout & Spacing
The layout system enforces a tight, fixed scale tailored to 360px–428px mobile viewport widths, ensuring key purchase details remain above the fold without cramped density.

### Spacing Scale
- **`4px` (`space-xs`):** Micro gaps between icons and labels, badge internal vertical padding.
- **`8px` (`space-sm`):** Spacing between grouped elements, input field internal vertical padding, chip margins.
- **`12px` (`space-md`):** Padding between card items, horizontal chip padding, text row vertical margins.
- **`16px` (`space-lg`):** Standard viewport edge margin, primary card interior padding, input field horizontal inset.
- **`24px` (`space-xl`):** Major section separation, vertical gap before sticky bottom navigation or CTA containers.

### Grid & Layout Rules
- **Margins & Safe Zones:** A uniform `16px` canvas edge margin is maintained across mobile viewports.
- **Vertical Stack Cadence:** List items maintain `8px` or `12px` internal padding with a `1px` divider (`#E6EAED`).
- **Touch Heights:** Standard interactive elements (buttons, form inputs, list rows) maintain an absolute minimum touch target height of `44px` to `48px`, even when text labels remain small.

## Elevation & Depth
This design system rejects heavy drop shadows, colored drop glows, and blurred materials. Visual planes are created through precise border encapsulation and high-contrast value shifts.

### Depth Rules
- **Base Canvas:** Viewports utilize `#F5F7F8` or `#FFFFFF`.
- **Card Containers:** Pure white (`#FFFFFF`) with a `1px solid #E6EAED` border. No drop shadows on standard cards.
- **Elevated Modals & Floating Elements:** Used sparingly for bottom sheets and floating action centers. A subtle, low-opacity neutral drop shadow is permitted:
  - `box-shadow: 0px 4px 12px rgba(7, 23, 36, 0.08);`
- **Dark Surface Accent:** Midnight (`#071724`) surfaces stand out directly through contrast without needing elevation tokens.

## Shapes
Geometry is disciplined, using compact corner radii to maintain high structural efficiency. Rounded pill shapes are prohibited on interactive inputs and buttons to sustain an organized, utility-focused mobile interface.

### Radius Assignments
- **Cards & Card Groups:** `8px`
- **Text Inputs & Selectors:** `8px`
- **Buttons (Primary, Secondary, Ghost):** `8px`
- **Dialogs & Alert Modals:** `8px`
- **QR Viewfinder & Barcode Framing Containers:** `8px`
- **Icon Containers & Tile Badges:** `8px`
- **Status Chips & Verification Tags:** `6px`
- **Bottom Sheets:** Top-left and top-right corners only: `12px` (`12px 12px 0px 0px`).

## Components

### Buttons
- **Primary Button:** Height `48px`, background `#0DB3A0`, label `#FFFFFF` (`13px / 600`), border-radius `8px`, no border. Active/Pressed state: `#0DB3A0` at 90% brightness.
- **Secondary Button:** Height `48px`, background `#FFFFFF`, border `1px solid #E6EAED`, label `#071724` (`13px / 600`), border-radius `8px`.
- **Scan Trigger Button:** Background `#FFB547`, label `#071724` (`13px / 600`), border-radius `8px`.
- **Destructive Button:** Background `#FFFFFF`, border `1px solid #EF6A6A`, label `#EF6A6A` (`13px / 600`).

### Chips & Badges
- **Status Chip Base:** Height `24px`, horizontal padding `8px`, corner radius `6px`, font `11px / 500`.
  - **Verified / Confirmed:** Background `#E6F7F5`, text `#0DB3A0`, border `1px solid #7AE1D6`.
  - **Pending Review:** Background `#FFF7EB`, text `#071724`, border `1px solid #FFB547`.
  - **Rejected / Expired:** Background `#FDECEC`, text `#EF6A6A`, border `1px solid #EF6A6A`.

### Text Inputs
- **Container:** Height `48px`, background `#FFFFFF`, border `1px solid #E6EAED`, border-radius `8px`, horizontal padding `16px`.
- **Typography:** Value `12px / 400` in `#071724`. Placeholder `12px / 400` in `#66737D`.
- **States:** 
  - Focused: border `1px solid #0DB3A0`.
  - Error: border `1px solid #EF6A6A`, with helper label `11px / 400` below in `#EF6A6A`.

### Cards & Containers
- **Content Card:** Background `#FFFFFF`, border `1px solid #E6EAED`, border-radius `8px`, padding `16px`.
- **Loyalty Summary Card:** Background `#071724`, border-radius `8px`, padding `16px`, primary value text `#FFFFFF` (`22px / 700`), helper labels `#7AE1D6` or `#E6EAED`.

### Lists & Dividers
- **Dividers:** Height `1px`, background `#E6EAED`, full bleed or inset `16px` to align with text margins.
- **List Items:** Min height `48px`, padding `12px 16px`, active state ripple `#F5F7F8`.

### Scanner HUD Viewfinder
- **Frame:** Centered container with an `8px` corner radius.
- **Guide Brackets:** Amber (`#FFB547`) corner indicators framing the scanning target. No glow, blur, or laser effects.
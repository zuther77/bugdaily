---
name: Cybernetic Diagnostic
colors:
  surface: '#10131b'
  surface-dim: '#10131b'
  surface-bright: '#353941'
  surface-container-lowest: '#0a0e15'
  surface-container-low: '#181c23'
  surface-container: '#1c2027'
  surface-container-high: '#262a32'
  surface-container-highest: '#31353d'
  on-surface: '#dfe2ed'
  on-surface-variant: '#bdc8d1'
  inverse-surface: '#dfe2ed'
  inverse-on-surface: '#2d3038'
  outline: '#87929a'
  outline-variant: '#3e484f'
  surface-tint: '#7bd0ff'
  primary: '#8ed5ff'
  on-primary: '#00354a'
  primary-container: '#38bdf8'
  on-primary-container: '#004965'
  inverse-primary: '#00668a'
  secondary: '#4ae176'
  on-secondary: '#003915'
  secondary-container: '#00b954'
  on-secondary-container: '#004119'
  tertiary: '#ffbcb7'
  on-tertiary: '#68000a'
  tertiary-container: '#ff938c'
  on-tertiary-container: '#8d0012'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#c4e7ff'
  primary-fixed-dim: '#7bd0ff'
  on-primary-fixed: '#001e2c'
  on-primary-fixed-variant: '#004c69'
  secondary-fixed: '#6bff8f'
  secondary-fixed-dim: '#4ae176'
  on-secondary-fixed: '#002109'
  on-secondary-fixed-variant: '#005321'
  tertiary-fixed: '#ffdad7'
  tertiary-fixed-dim: '#ffb3ad'
  on-tertiary-fixed: '#410004'
  on-tertiary-fixed-variant: '#930013'
  background: '#10131b'
  on-background: '#dfe2ed'
  surface-variant: '#31353d'
typography:
  headline-lg:
    fontFamily: Inter
    fontSize: 28px
    fontWeight: '700'
    lineHeight: 34px
    letterSpacing: -0.02em
  headline-md:
    fontFamily: Inter
    fontSize: 22px
    fontWeight: '600'
    lineHeight: 28px
    letterSpacing: -0.01em
  headline-sm:
    fontFamily: Inter
    fontSize: 18px
    fontWeight: '600'
    lineHeight: 24px
  body-lg:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  body-sm:
    fontFamily: Inter
    fontSize: 12px
    fontWeight: '400'
    lineHeight: 16px
  code-lg:
    fontFamily: JetBrains Mono
    fontSize: 15px
    fontWeight: '500'
    lineHeight: 24px
  code-md:
    fontFamily: JetBrains Mono
    fontSize: 13px
    fontWeight: '400'
    lineHeight: 20px
  code-sm:
    fontFamily: JetBrains Mono
    fontSize: 11px
    fontWeight: '400'
    lineHeight: 16px
  label-md:
    fontFamily: JetBrains Mono
    fontSize: 12px
    fontWeight: '600'
    lineHeight: 16px
    letterSpacing: 0.04em
  label-sm:
    fontFamily: JetBrains Mono
    fontSize: 10px
    fontWeight: '600'
    lineHeight: 14px
    letterSpacing: 0.05em
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  gutter: 0.75rem
  margin: 1rem
  space-xs: 0.25rem
  space-sm: 0.5rem
  space-md: 0.75rem
  space-lg: 1rem
  space-xl: 1.5rem
---

## Brand & Style

This design system establishes an authentic, razor-sharp IDE aesthetic optimized for mobile tactile interaction. Designed specifically for software engineers and code enthusiasts playing a daily diagnostic game, it treats the viewport not as a generic gamified canvas, but as a sleek, hyper-specialized mobile terminal.

The aesthetic fuses **Modern Technical Dark Mode** with **Precision IDE UI**:
- Surfaces reflect the deep slate and zinc depths of high-performance code editors.
- High-contrast syntax tokens transform code fragments into actionable, tap-ready targets.
- Haptic and visual precision replaces playful fluff: correct taps deliver instant terminal verification, while erroneous taps manifest as subtle compiler faults and red-tinted diagnostics.
- Touch ergonomic standards maintain strict adherence to mobile tap boundaries (44px minimum target footprint) disguised within native code lines and gutter markers.

## Colors

The palette directly models real-world developer environments while adhering to WCAG 2.1 AAA contrast ratios across pitch-dark backgrounds.

### Core Canvas & Surfaces
- **Canvas Base (`#0c1017`)**: Deepest substrate; used for the root viewport, background framing, and inactive notch/status bar extensions.
- **Surface Elevation 1 (`#0d1117`)**: Editor gutter, line-number tracks, and secondary chrome panels.
- **Surface Elevation 2 (`#151b23`)**: Active code block surface, inspectable card modules, and bottom sheet containers.
- **Surface Elevation 3 (`#212830`)**: Hover/press overlays, tab active indicators, and interactive code token pills.

### Accent & Functional Roles
- **Selection & Focus (`#38bdf8`)**: Electric Cyan. Guides user attention, highlights active cursor lines, selections, and primary CTA buttons.
- **Success & Verified Bug (`#22c55e`)**: Emerald Green. Used exclusively for correctly pinpointed bugs, passing tests, and streak increments.
- **Failure & Compiler Error (`#ef4444`)**: Crimson Red. Signals false selections, syntax runtime errors, and failed attempts.
- **Warning & Attention (`#f59e0b`)**: Amber Orange. Denotes lint warnings, hints remaining, timer urgency states, and modified diff lines.

### Syntax Spectrum
- **Keywords / Logic**: `#f472b6` (Pink)
- **Functions / Calls**: `#60a5fa` (Cobalt)
- **Strings / Constants**: `#a3e635` (Lime)
- **Variables / Types**: `#fb923c` (Tangerine)
- **Comments / Line Numbers**: `#656c76` (Muted Slate)

## Typography

Typography establishes an absolute separation between the game interface and the code artifact being analyzed:

1. **System & Interaction UI (`Inter`)**: All menus, challenge briefs, streak counters, and modal triggers render in clean, neutral grotesque type with tight tracking. This ensures high structural legibility without clashing against the monospace code payload.
2. **Terminal & Game Artifacts (`JetBrains Mono`)**: All code snippets, diff inspectors, token selectors, line numbers, and metric counters use monospaced letterforms. JetBrains Mono provides clear character disambiguation (e.g., `0` vs `O`, `l` vs `1`) crucial for debugging tasks on handheld screens.

### Line Height Constraints for Mobile Touch
The `code-lg` level is the canonical size for interactive code lines. To conform to accessibility parameters, every code line uses a minimum height container of `44px` on mobile tap regions, while the visual typeface remains set at `15px` with a `24px` font line height, padded evenly to avoid mis-taps.

## Layout & Spacing

The layout is engineered around the standard `390x844` portrait iPhone viewport, maximizing vertical code presentation while retaining dedicated touch regions.

### Structure & Safe Areas
- **Top Bar**: Fixed `52px` header containing challenge metadata, daily streak counter, and remaining attempt tokens.
- **Main Code Canvas**: Vertically scrollable code editor container bordered by a pinned `36px` line-number gutter on the left.
- **Docked Action Bar**: A pinned `68px` bottom panel floating `16px` above the iOS Home Indicator containing diagnosis controls, submit verification, and hint buttons.
- **Outer Margins**: Strict `16px` (`margin`) outer screen buffer preventing accidental edge swipes on curved device displays.
- **Column Gaps**: `12px` (`gutter`) separation for split diff views and comparative debug tiles.

## Elevation & Depth

This system avoids blurred drop shadows in favor of flat architectural depth, low-opacity strokes, and crisp structural hierarchy.

### Tonal Hierarchy
- **Canvas Base (`#0c1017`)**: Lowest tier; background environment.
- **Editor Frame (`#151b23`)**: Layer 1 elevation; bounded by a 1px border (`#30363d`).
- **Active Inspection Row**: Layer 2 elevation; rendered with background `rgba(56, 189, 248, 0.08)` and a left border of `3px solid #38bdf8`.
- **Bottom Navigation Dock**: Frosted glass depth (`#151b23` with 90% opacity, `backdrop-filter: blur(16px)`), bordered by a top stroke (`1px solid #30363d`).

### Interactive Feedback Layers
- **Error State**: Active line shifts background to `rgba(239, 68, 68, 0.12)` with a border outline of `1px solid #ef4444`.
- **Success State**: Active line shifts background to `rgba(34, 197, 94, 0.12)` with a border outline of `1px solid #22c55e`.

## Shapes

The shape vocabulary uses compact, technical roundedness (`0.25rem` / `4px` base radius), matching modern developer tooling and IDE tab bars.

- **Buttons & Control Chips**: `4px` corner radius (`rounded-sm`) to retain an industrial, instrument-grade appearance.
- **Code Container**: `8px` (`rounded-lg`) corner radius with clipped overflows.
- **Modal Sheets & Overlays**: `12px` (`rounded-xl`) on top edges to provide gentle ergonomics during pull-up actions.
- **Token Target Pills**: `4px` rounded inline highlights wrapped tightly around suspect code segments.

## Components

### 1. Interactive Code Line / Token (Primary Tap Target)
- **Geometry**: Minimum height of `44px` per touch line; full-width clickable tap row.
- **Default State**: Gutter line number in `#656c76`, syntax highlighting across tokens, transparent background.
- **Selected State**: Tinted with `#38bdf8` at 10% opacity, 1px dashed outline `#38bdf8`.
- **Confirmed Bug**: `#22c55e` filled background at 15%, solid `#22c55e` 1px border, bug icon badge on gutter.
- **False Positive**: `#ef4444` background at 15%, quick 3-cycle horizontal micro-shake animation, strike-through text decoration.

### 2. Buttons
- **Primary Action (Confirm Diagnosis)**: Full width inside the bottom dock, height `48px`, background `#38bdf8`, label in `JetBrains Mono` bold 13px uppercase with `#0c1017` text.
- **Secondary Action (Hint / Reset)**: Height `48px`, background `transparent`, border `1px solid #30363d`, text `#f59e0b`.
- **Icon Buttons (File switcher, Settings)**: `44x44px` touch bounding box, icon rendered at `20px` in `#8b949e`.

### 3. Metric Badges & Chips
- **Streak & Time Counter**: Height `28px`, background `#151b23`, border `1px solid #30363d`, text in `JetBrains Mono` 11px, flex row with leading colored indicator dot (`#22c55e` for live streak).

### 4. Code Diff Card
- **Layout**: Enclosed box with `#151b23` background and `#30363d` 1px border. Header toolbar showing file name (e.g., `main.rs`, `query.ts`) and modified line delta (`+1 / -1`).
- **Gutter**: 36px wide with `#0d1117` background and 1px right border separating code text.

### 5. Compiler Diagnostic Toast
- **Anchoring**: Appears directly below the docked header, height auto, padding `12px 16px`.
- **Theme**: Monospaced terminal output box with `#0d1117` background, 1px left accent bar (`#ef4444` on error, `#f59e0b` on hint).
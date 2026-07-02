# Mixed Productivity UI Redesign Design

Date: 2026-07-02

## Goal

Redesign the app UI across desktop, Android phone, and Android tablet into a mixed light/dark productivity workspace. The redesign should make the canvas feel like the primary work surface, keep configuration tasks readable and efficient, and remove the current visual noise from glassy surfaces, overly decorative backgrounds, and inconsistent platform density.

## Approved Direction

Use a mixed productivity interface:

- Light configuration surfaces for prompt entry, model settings, upload controls, and generation actions.
- Dark graphite canvas workspace for preview, drawing, toolbar, source strip, and status context.
- Compact desktop-tool proportions instead of marketing-style spacing.
- Unified visual language across desktop, Android phone, and Android tablet, with platform-specific layout behavior.
- Accent palette centered on teal/green for primary action, amber for waiting/warning state, and red for destructive or failed state.

## Layout

### Desktop

The desktop shell remains structurally composed from `ControlPanel`, `canvas-shell`, and `HistoryRail`, but the proportions and visual hierarchy change.

- Left panel: fixed, compact configuration column around 350-380px.
- Center: flexible dark canvas workspace with the strongest visual weight.
- Right rail: narrower history/material rail around 240-280px.
- Fullscreen mode continues to hide side panels and focus only on the canvas.
- Header height is reduced and styled as a tool title bar.
- Workspace bar remains available but becomes visually quieter and more integrated with the header area.

### Android Phone

The phone layout uses a workflow switch instead of compressed multi-column layout.

- Compose view: light configuration screen.
- Canvas view: dark work surface with mobile-friendly toolbar and status treatment.
- History view: dedicated asset/history screen.
- Spacing stays touch-friendly while sharing the same color tokens and control shapes as desktop.

### Android Tablet

Tablet layout uses the same mixed light/dark language but adapts by width.

- Expanded tablet: two or three column workspace, close to desktop.
- Medium tablet: primary canvas plus one active side panel.
- Compact tablet: same workflow view logic as phone.

## Components

### Header

The header becomes a compact product toolbar:

- Keep app identity, platform switching, and necessary controls.
- Keep previously removed GitHub/star promotional controls absent.
- Reduce ornamental styling and avoid large gradients.
- Preserve draggable window regions and existing platform-specific behaviors.

### Control Panel

The control panel becomes a light inspector/configuration surface:

- Prompt editor and settings are grouped with tighter rhythm.
- Inputs and buttons use 6-8px radius, clear borders, and stable heights.
- Primary generation action uses teal/green.
- Secondary actions use neutral styling.
- Destructive or risky actions use restrained red.

### Canvas

The canvas shell becomes the central dark workspace:

- Use a dark graphite background around the preview area.
- Toolbar, source strip, stage, and status bar read as one work surface.
- Empty state remains visible without becoming a landing-page hero.
- Borders and shadows are subtle and functional.

### History

History becomes a material rail:

- Desktop history is narrower and denser.
- Thumbnails use consistent aspect handling and stable grid sizing.
- Item controls are lighter and less card-like.
- Phone history remains a full view for readability.

## Styling Architecture

The implementation should keep the existing CSS architecture and avoid a broad rewrite.

- Update global design tokens in `src/styles/index.css`.
- Update layout rules in `src/styles/_layout.css`.
- Update panel rules in `src/styles/_panel.css`.
- Update canvas rules in `src/styles/_canvas.css`.
- Update history rules in `src/styles/_history.css`.
- Update Android-specific files only where needed for phone/tablet layout and color consistency.
- Preserve existing class names where practical so state and tests do not need unnecessary rewiring.

## Testing And Verification

Add or update focused tests before implementation changes where behavior or structural expectations change.

Required verification:

- Promotional GitHub/star controls remain absent.
- Legacy brand strings remain absent.
- Header, workspace, desktop shell, canvas shell, and history rail still render through expected structural classes.
- Android phone and tablet layout selectors remain present and do not collapse into desktop-only assumptions.
- Run targeted Node tests for prior branding/configuration changes.
- Run `npm run build:windows` from `image-studio/frontend`.

Known constraint:

- Full `npm test` has existing TypeScript loader issues in this environment, so final verification should use targeted runnable tests plus the Windows build unless that environment issue is separately fixed.

## Non-Goals

- Do not change image generation API behavior.
- Do not reintroduce removed FHL, GitHub, or star promotional content.
- Do not rewrite state management.
- Do not replace React/Wails architecture.
- Do not create a landing page or marketing hero.
- Do not add new branding assets unless required by the redesign.

## Acceptance Criteria

- Desktop, phone, and tablet all share the same mixed productivity visual language.
- The canvas is visually dominant and clearly separated as a dark work surface.
- Configuration remains readable on light surfaces.
- Main actions and status states use the new restrained accent system.
- Layout remains responsive and avoids overlapping text or controls.
- Targeted tests and Windows frontend build complete with the expected results.

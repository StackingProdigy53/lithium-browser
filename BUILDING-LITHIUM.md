# Building Lithium

Lithium is a Chromium-based browser. This repository contains the patches,
resources, and configuration that turn upstream Chromium/ungoogled-chromium
into Lithium builds.

## Prerequisites
- A working Chromium/ungoogled-chromium build environment for your OS.
- Access to the platform packaging repos:
  - macOS: https://github.com/imputnet/lithium-macos
  - Linux: https://github.com/imputnet/lithium-linux
  - Windows: https://github.com/imputnet/lithium-windows

## High-level build flow
1. Sync Chromium/ungoogled-chromium sources for the target version.
2. Apply Lithium patches from this repository.
3. Copy Lithium resources into the Chromium tree (icons, branding, etc.).
4. Build and package using the platform packaging repo for your OS.

## Notes
- Platform repos handle installer packaging and platform-specific build scripts.
- When updating UI or themes, ensure resource mappings are refreshed so the
  build outputs include the updated assets.
docs/OVERHAUL.md
docs/OVERHAUL.md
New
+69
-0

# Lithium Full Overhaul Plan

This document tracks the full UI/UX, branding, and theming overhaul for Lithium.
It is intended to make the browser feel cohesive across platforms while
preserving Chromium stability and performance.

## Goals
- Deliver a unified visual language across the UI surfaces (toolbar, menus,
  settings, onboarding, and web UI pages).
- Provide a skinning system that supports both first-party themes and external
  styling tools (including WindowBlinds 11 on Windows).
- Reduce friction for packaging so the source tree can be built into a fully
  working browser across supported platforms.

## Scope
### UI
- Toolbar, tab strip, omnibox, window frame, and window controls.
- Settings, customize Chrome side panel, and in-product dialogs.
- New tab page and onboarding.

### Skins
- Skin bundles for light/dark, high-contrast, and branded palettes.
- Resource mapping for icons, favicons, and UI glyphs.
- Token-based colors, spacing, and corner radii that can be swapped per skin.

### Platform compatibility
- Windows: WindowBlinds 11 compatibility and native theme alignment.
- macOS: native vibrancy and system accent color respect.
- Linux: GTK theme alignment and system font consistency.

## WindowBlinds 11 Compatibility Checklist (Windows)
1. **Prefer native theme colors**
   - Use OS-provided system colors where possible (avoid hard-coded grays).
   - Respect user high-contrast settings.
2. **Avoid forcing custom frame painting**
   - Keep window frames and title bar using native APIs unless necessary.
   - When custom frames are required, expose toggles to fall back to native.
3. **Expose theming toggles**
   - Provide flags or settings that allow users to:
     - Enable/disable custom frame.
     - Toggle use of system colors.
     - Select skin presets that map to WindowBlinds-friendly values.
4. **Test matrix**
   - WindowBlinds 11 default skins.
   - High-contrast and custom system palettes.
   - Dark/Light OS modes with accent color changes.

## Implementation Roadmap
### Phase 1 — Baseline cleanup
- Inventory existing patches that adjust UI and theming.
- Consolidate theme tokens and remove redundant overrides.

### Phase 2 — Skinning system
- Define theme token map for colors, radii, spacing.
- Build a skin registry that can map token values to brand presets.
- Update UI surfaces to consume tokens instead of hard-coded styles.

### Phase 3 — Platform-specific theming
- Windows: adopt native colors and expose custom frame toggles for
  WindowBlinds compatibility.
- macOS/Linux: align to native system appearance and font metrics.

### Phase 4 — Packaging and delivery
- Ensure build docs are up to date for all platforms.
- Validate default configuration and branding assets.

## Tracking
- Each patch or change related to the overhaul should reference this document
  in its commit or patch description so the work remains coordinated.

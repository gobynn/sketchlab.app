# Sketch Lab — project context

## Purpose
Sketch Lab is a parked Adam-owned local-first diagram experiment retained for renderer and product-reference work. Excalidraw is Adam’s default diagram tool. Do not select Sketch Lab for normal diagrams unless Adam explicitly asks to work in this repository or asks for Sketch Lab by name.

## Build and test
- Install from the committed lockfile: `npm ci --ignore-scripts`.
- Before claiming a code change works, run `npm run build` and `npm test`.
- Keep the working tree clean except for intentional, reviewed changes.

## Architecture
- `src/state/` — board data types, generated-graph validation, mutations.
- `src/render/` — PixiJS scene and visual rendering.
- `src/interaction/` — pointer, keyboard, camera, and editing behavior.
- `src/persistence/` — IndexedDB and URL import/share behavior.
- `src/ui/` — dashboard, editor controls, panels, and browser UI.
- `test/` — Vitest regression tests.

## Agent diagrams
Only when Adam explicitly asks for Sketch Lab, read `docs/hermes-diagrams.md`. Generate a concise valid `GeneratedGraph`, then open it with the local `?g=` URL. For normal diagram requests, direct the work to Excalidraw and `~/shebang/tools/excalidraw-workflow.md`. Do not use Mermaid as an intermediary, invent icon names, or include sensitive KRD/HR information.

## Ownership and upstream
- `origin` is `gobynn/sketchlab.app`: Adam’s fork and the only push target.
- `upstream` is `webdevcody/sketchlab.app`: inspect and selectively merge upstream changes; do not push there.
- Preserve local-first behavior and never add credentials to source control.

## Feature work
- Start feature work with a small written behavior/design decision when it affects persisted board data, rendering, interaction, or generated-graph compatibility.
- Add focused regression tests for changed behavior and preserve loading of older boards.
- The first proposed owned feature is documented at `docs/arrow-styles-design.md`; do not implement it until Adam confirms the style set.

# Sketch Lab — project context

## Purpose
Sketch Lab is Adam’s local-first diagram workspace. It helps Hermes explain systems, programming, Apple-platform workflows, and other visual ideas through editable boards. Boards remain in the browser’s IndexedDB unless Adam deliberately shares a generated URL.

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
When Adam asks for a Sketch Lab diagram, read `docs/hermes-diagrams.md`. Generate a concise valid `GeneratedGraph`, then open it with the local `?g=` URL. Do not use Mermaid as an intermediary, invent icon names, or include sensitive KRD/HR information.

## Ownership and upstream
- `origin` is `gobynn/sketchlab.app`: Adam’s fork and the only push target.
- `upstream` is `webdevcody/sketchlab.app`: inspect and selectively merge upstream changes; do not push there.
- Preserve local-first behavior and never add credentials to source control.

## Feature work
- Start feature work with a small written behavior/design decision when it affects persisted board data, rendering, interaction, or generated-graph compatibility.
- Add focused regression tests for changed behavior and preserve loading of older boards.
- The first proposed owned feature is documented at `docs/arrow-styles-design.md`; do not implement it until Adam confirms the style set.

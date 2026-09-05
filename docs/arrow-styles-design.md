# Arrow styles — proposed design

> Status: proposed. This records Adam’s first owned feature request; it is not implemented yet.

## User problem

A connector currently renders as either a straight line or a quadratic bend controlled by one midpoint handle. A directed connector always uses the same filled arrowhead. Adam wants the arrow tool to provide clear style choices—such as curved and square-cornered routes—rather than a single visual language.

## First release: keep choices understandable

Separate two decisions in the UI. Users should not have to learn one large “arrow style” menu.

### Route

| Choice | Meaning | Existing data impact |
|---|---|---|
| Straight | Direct line from source to target. | Existing default; no control point. |
| Curved | Smooth quadratic curve, adjustable with the existing bend handle. | Existing `cx` / `cy` behavior. |
| Elbow | Orthogonal route with square corners, useful for architecture and flow diagrams. | New persisted route mode and computed/manual waypoints. |

### End marker

| Choice | Meaning |
|---|---|
| None | Plain connector. |
| Filled arrow | Current directed-arrow default. |
| Open arrow | Outline arrowhead for lighter relationships. |
| Diamond | Composition/data-object relationship. |
| Circle | Event or source marker. |
| Bar | A terminal/stop marker. |

The first implementation should support an end marker only. Start markers and double-ended arrows can be a later addition after real use proves they are needed.

## Interaction

1. Selecting an edge reveals a compact **Line** inspector beside the existing edge controls.
2. The inspector has a route segmented control: `Straight | Curved | Elbow`.
3. It has a marker picker with visual previews, not text-only labels.
4. Keyboard shortcut behavior remains unchanged: `L` starts a plain connector and `A` starts a filled-arrow connector.
5. Changing a route never loses the edge label, color, source, target, or layer.
6. For an elbow edge, dragging the middle handle should adjust the orthogonal path without creating diagonal segments.

## Technical direction

The current `Edge` model has `directed?: boolean` and optional `cx` / `cy`; `edgeView.ts` renders one straight or quadratic path and a fixed filled arrowhead. The smallest compatible extension is:

```ts
type EdgeRoute = "straight" | "curve" | "elbow";
type EdgeMarker = "none" | "arrow-filled" | "arrow-open" | "diamond" | "circle" | "bar";

interface Edge {
  // existing fields remain valid
  route?: EdgeRoute;       // absent means inferred from old boards: curve when cx/cy exist, else straight
  endMarker?: EdgeMarker;  // absent means arrow-filled when directed, otherwise none
}
```

Compatibility rule: older boards must render exactly as they did before the feature. `directed` remains supported during migration; the UI writes `endMarker` for new edits.

## Acceptance criteria before implementation is complete

- Existing boards load with the same connector appearance.
- A new edge can use every first-release route and marker.
- The hit area, selection, dragging, labels, auto-layout, copying, undo/redo, sharing, and persisted boards work for every route.
- GeneratedGraph imports retain their current behavior; agent-generated directed edges initially map to `arrow-filled`.
- Focused Vitest coverage proves back-compat, geometry output, route conversion, and marker rendering choices.
- `npm run build` and `npm test` pass.

## Deliberately not in version one

- Manual multi-segment routing.
- Arbitrary SVG marker uploads.
- Dashed or animated line styles.
- Start markers or double-ended arrows.
- Auto-avoidance around every shape.

Those can be considered after the simple route/marker model is used in real diagrams.

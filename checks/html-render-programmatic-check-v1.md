# HTML Render / Programmatic Check v1

## Scope
Artifact checked: `slides/index.html`

## Programmatic checks

| Check | Result | Notes |
|---|---|---|
| HTML file exists | PASS | `slides/index.html` exists. |
| Slide count | PASS | 13 slides, within the required 12–15 range. |
| Source footer | PASS | 13/13 slides contain a visible source footer. |
| Slide counter | PASS | 13/13 slides contain a page counter. |
| Required Evidence Cards exist | PASS | 6/6 Evidence Cards are present. |
| Required Wiki entries exist | PASS | Concept, dataset, method, and metric entries referenced by the deck are present. |
| Browser interaction code present | PASS | Previous/next buttons, keyboard navigation, hash state, and progress bar are included. |
| Printable rendering | PASS | WeasyPrint successfully rendered the deck to 13 PDF pages. |

## Rendering check

A 13-page render was generated as `slides/render-check.pdf`, then converted into a montage at `slides/render-check-montage.png` for visual inspection.

### Visual result
- 13/13 slides rendered.
- No obvious text clipping was found.
- No card or table visibly crossed the slide boundary.
- Source footers and slide counters remained inside the slide area.
- Tables on Slides 3, 8, and 11 remained readable in the rendered layout.

## Notes
The HTML uses a responsive browser layout and a separate print rendering rule for deterministic 16:9 inspection. Browser navigation is handled by JavaScript; the print render intentionally shows all slides sequentially.

## Final Status
**PASS**

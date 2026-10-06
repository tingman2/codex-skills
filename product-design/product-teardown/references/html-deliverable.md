# HTML deliverable specification

Generate one self-contained, navigable HTML report. Adapt section depth to the product archetype and the user's scope; do not fabricate empty architecture merely to fill a template.

## Required report sections

1. Executive summary — one sentence explaining the product's core mechanism and the strongest evidence-backed finding.
2. Scope and evidence readiness — sources inspected, chronology, inaccessible evidence, and limits.
3. Product classification — primary/secondary archetype, rationale, and analysis emphasis.
4. Core user promise and functional domains.
5. User layer — journey, decisions, emotions, friction, recovery, and visible completion.
6. Technology layer — workbench, application domains, orchestration, tools/services, state, safety, billing, and observability at supported confidence.
7. Model layer — modalities, named models and parameters, routing/selection, constraints, cost/latency/quality, safety, and unknowns.
8. Data layer — contexts, business entities, assets, references, versions, workflow state, confirmations, errors, billing, feedback, and public/private boundaries.
9. End-to-end cross-layer flow — trigger, reader, decision, tool, output, state write, confirmation, handoff, and failure branch.
10. Current architecture (`As-Is`).
11. Recommended architecture (`To-Be`).
12. Risks and validation priorities.
13. Component-to-evidence traceability table.
14. Unknowns and next evidence to collect.

Add agent I/O contracts, state machines, ER diagrams, sequence diagrams, knowledge architecture, or model-routing details only when relevant to the product and supported by the requested scope.

## Presentation rules

- Use inline CSS and no build step.
- Provide sticky navigation for long reports.
- Use responsive cards and horizontally scrollable tables/large diagrams.
- Make evidence IDs visually distinct and repeat them near the claims they support.
- Use consistent badges for `事实`, `推断`, `建议`, and `未知`.
- Include a visible legend.
- Use real page labels and asset names only when evidence supports them.
- Put architectural template names in a note saying they are analytical names, not confirmed internal identifiers.
- Make dense diagrams scrollable at a readable scale rather than shrinking labels to illegibility.

## Diagram semantics

When diagrams materially improve comprehension:

- use solid lines for observed interactions/results;
- use dashed lines for inferred mechanisms;
- use dotted or a distinct accent for recommended design;
- label edges with `调用`, `读取`, `写入`, `事件`, `确认`, `资产引用`, or `状态更新` as appropriate;
- show conflicts and missing validation gates explicitly;
- include a legend and evidence IDs on important nodes.

Mermaid is acceptable. Preserve the Mermaid source in the HTML and render-check every diagram. If using a CDN, note that diagrams need network access; prefer embedded rendering when the environment can provide it.

## Visual QA

Before delivery:

1. parse the HTML;
2. open it in a browser;
3. confirm navigation and all required sections;
4. confirm tables do not overflow without scrolling;
5. verify every Mermaid diagram renders without syntax errors;
6. inspect at least the top, one dense table, and the main architecture diagram;
7. remove stale, hidden, or contradictory draft content;
8. return an absolute clickable path to the final HTML.

---
name: product-teardown
description: Evidence-first teardown of digital products, including AIGC creation tools, execution agents, conversational companions, and hybrid products. Use when the user asks to reverse-analyze product workflows, agents, tools, models, data, architecture, risks, or improvement opportunities from screenshots, a live website, source code, or other first-party product evidence, with the final deliverable as HTML.
---

# Product Teardown

Produce a product teardown that separates observed behavior from inferred architecture and recommended design. Never carry a prior product's names, entities, agent roster, or workflow into a new teardown.

## Evidence gate

Do not begin substantive teardown conclusions until at least one inspectable product-evidence source is available. Acceptable sources include:

- a sufficiently complete, ordered screenshot set or screen recording;
- a reachable product URL and authorization to inspect it;
- original source code or a repository/workspace;
- exported conversations, project data, product documentation, or API results that expose the product behavior in scope.

If evidence is absent, inaccessible, unordered, or too narrow for the requested scope, stop after an evidence-readiness assessment. State what is present, what it can support, and the minimum missing evidence required. Do not fill gaps with product marketing, generic industry knowledge, or a previous teardown.

Read [references/evidence-protocol.md](references/evidence-protocol.md) whenever collecting, auditing, or citing evidence.

## Classify before decomposing

Infer the product's primary archetype and any secondary archetype from the evidence. Do not classify from the user's label alone. Read [references/product-archetypes.md](references/product-archetypes.md), select the relevant emphasis, and state why.

The archetype changes the teardown center of gravity:

- AIGC creation products: creative stages, confirmation gates, asset lineage, consistency, media models, cost, versions, and final-output validation.
- General execution agents: intent-to-plan-to-action control, tool authorization, side effects, state, observability, interruption, retry, idempotency, and completion proof.
- Conversational companions: persona, memory, relationship continuity, emotional adaptation, privacy, safety boundaries, escalation, retention mechanics, and user control.
- Hybrid products: identify which subsystem owns the main user promise; apply other emphases only where evidence supports them.

## Work in four layers

Always organize the analysis around these four layers. They are analytical views, not claims about the product's actual implementation.

1. **User layer** — entry points, user goals, journey, decisions, emotions, friction, permissions, interruption, recovery, and visible outcomes.
2. **Technology layer** — UI/workbench, application domains, agent or workflow orchestration, tool/service calls, asynchronous jobs, state machine, asset services, security, billing, and observability.
3. **Model layer** — model roles, named models, selectable parameters, routing evidence, modality, constraints, safety, latency/cost tradeoffs, fallbacks, and quality validation.
4. **Data layer** — user context, project context, conversations, structured entities, assets and versions, references and dependencies, workflow state, confirmations, errors, billing, feedback, privacy, and public/private knowledge boundaries.

Within each layer, label every conclusion:

- `【页面/代码事实】` — directly observable and reproducible;
- `【合理推断】` — explains multiple facts but is not directly visible;
- `【建议设计】` — an improvement, not a current-product claim;
- `【未知】` — evidence is insufficient or conflicting.

Never upgrade an agent's statement such as “completed” into a fact without checking the corresponding asset, state, or output. Record conflicts instead of choosing one source as truth.

## Execution workflow

1. Restate the requested scope and readonly/mutation boundary.
2. Inventory evidence, assign stable evidence IDs, establish chronology, and list access gaps.
3. Classify the product and choose archetype-specific emphasis.
4. Trace one representative end-to-end task through user interaction, control, tools, data/state, and assets/results.
5. Decompose user, technology, model, and data layers. Identify cross-layer handoffs and evidence conflicts.
6. Describe the current architecture (`As-Is`) separately from inferred mechanisms and recommended architecture (`To-Be`).
7. Produce risk, validation, and evidence-traceability tables. Use `Unknown` rather than invented implementation details.
8. Generate a single HTML report and render it for visual QA. Read [references/html-deliverable.md](references/html-deliverable.md) before writing the report. Reuse [assets/report-template.html](assets/report-template.html) when practical.

## Operational boundaries

- Inspect product interfaces and repositories read-only unless the user separately authorizes changes.
- Do not trigger generation, regeneration, publishing, deletion, payment, purchase, recharge, or other material side effects merely to gather evidence.
- Never inspect or expose passwords, cookies, tokens, authorization headers, browser storage, or unrelated personal information.
- Public planning/thinking summaries are observable UI evidence, not hidden chain-of-thought and not proof that a tool ran.
- Use first-party product pages or official documentation for external supplementation. Treat marketing claims as claims, not verified behavior.
- Do not invent official tool names, prompts, database table names, model routing, vendors, programming languages, cloud services, or infrastructure.
- Functional tool names are allowed only when marked “functional name, not an official tool name.”
- When reviewing agents, summarize observable functional decisions. Never claim to recover hidden reasoning or an official system prompt.

## Completion standard

The teardown is complete only when:

- the evidence range and gaps are explicit;
- the product classification and resulting emphasis are justified;
- all four layers are covered at a depth supported by evidence;
- key cross-layer flows have evidence IDs;
- current facts, inferences, recommendations, and unknowns remain visibly separate;
- the HTML contains the requested scope, evidence traceability, `As-Is`, `To-Be`, risks, and unresolved questions;
- the HTML renders without broken layout or diagram errors.

Return a link to the HTML artifact and a short summary of the most important finding and evidence limitations.

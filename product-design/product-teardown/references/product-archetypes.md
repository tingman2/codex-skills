# Product archetype router

Use evidence to select one primary archetype and zero or more secondary archetypes. State the classification, evidence, and confidence. If two archetypes are equally central, describe the product as a hybrid and define which user promise belongs to each subsystem.

## AIGC creation product

Strong signals: prompt/script input, style selection, reference media, creative roles, generated images/video/audio/3D, canvas/timeline, variants, regeneration, asset library, preview/export.

Prioritize:

- journey from intent to final consumable output;
- stage gates and user confirmations;
- script/character/scene/prop/storyboard or equivalent creative entities;
- asset creation, lineage, reuse, consistency, invalidation, and versions;
- text/image/video/audio model responsibilities and exposed choices;
- asynchronous generation, progress, failure, cost, moderation, and final quality checks;
- mismatch between conversational claims, task state, canvas state, and stored assets.

Do not assume the product uses multiple agents merely because the process has multiple creative stages.

## General execution agent

Strong signals: user goal, plan, tool permissions, actions against external systems, task queue, execution logs, approvals, retries, completion report.

Prioritize:

- goal interpretation and plan formation;
- planner/executor/verifier separation only when evidenced;
- permission boundaries and human approval before side effects;
- tool I/O contracts, credentials boundary, state updates, and external effects;
- task lifecycle, asynchronous waits, interruption, cancellation, retry, rollback, idempotency;
- proof of completion versus an agent's narrative claim;
- audit log, traceability, failure recovery, and cost/usage control.

Do not treat a natural-language plan as proof that an external action occurred.

## Conversational companion

Strong signals: persistent persona, emotional or relationship framing, long-running dialogue, memory/personalization, proactive check-ins, safety or well-being handling.

Prioritize:

- persona consistency and relationship contract;
- short-term conversation context versus durable memory;
- consent for memory, correction, deletion, and privacy boundaries;
- emotion detection/adaptation without overclaiming mental-state knowledge;
- safety boundaries, crisis/escalation behavior, dependency risk, and age controls;
- proactive messaging, notification consent, retention mechanics, and user agency;
- response latency, voice/avatar modalities, and model personality controls.

Do not infer clinical capability, emotional understanding, or durable memory merely from empathetic language.

## Workflow/SaaS/data product

Strong signals: structured records, dashboards, forms, roles, approvals, reports, integrations, search/filter, and CRUD workflows.

Prioritize:

- domain objects and permissions;
- state transitions and business rules;
- data import/export, integrations, audit history, collaboration, and reporting;
- reliability, bulk operations, data quality, and access control.

## Classification questions

1. What outcome is the user paying time or money to obtain?
2. Is the main result content, an executed action, an ongoing relationship, or structured work/data?
3. Where does irreversibility or cost occur?
4. What must persist across sessions?
5. What is the strongest visible success criterion?

Use the answers to adjust emphasis; do not force every product through every optional module.

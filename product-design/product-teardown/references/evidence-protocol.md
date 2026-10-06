# Evidence protocol

## Readiness gate

Before analysis, build an evidence inventory with:

| Source | Availability | Coverage | Chronology | Reliability | Can support | Cannot support |
|---|---|---|---|---|---|---|

Evidence is ready only when it can support the user's requested scope. A homepage screenshot may support entry-point analysis but not an end-to-end workflow. A code repository may support implementation facts but not actual production behavior. A live authenticated workspace may support visible behavior but not invisible backend choices.

If evidence is insufficient, ask for the smallest useful addition, such as:

- ordered screenshots from first input through final output and failure states;
- the exact product/project URL with current access;
- the relevant repository or source directory;
- exported conversation/task history;
- official model, billing, permission, or error documentation.

## Evidence identifiers

Assign stable IDs by source type:

- `Sxx`: screenshot or video frame;
- `Pxx`: visible page state or UI observation;
- `Cxx`: code location or reproducible code result;
- `Dxx`: official document;
- `Rxx`: runtime/tool result;
- `Exx`: error or conflict record.

Each evidence record should contain source location, timestamp/order when known, visible original text, relevant controls/assets/state, and what it proves. Do not reuse one ID for unrelated observations.

## Chronological collection

For workflow products, begin with the earliest visible event and inspect in order:

1. original user intent and attachments;
2. first product response and any plan summary;
3. parameter collection and confirmation gates;
4. each user choice or correction;
5. visible tool/asset/task results;
6. downstream handoff;
7. final preview/export or stopping point;
8. failures, cancellation, insufficient balance, moderation, retry, and recovery when present.

Inspect chat, buttons/forms, canvas/cards, asset history, task state, previews, errors, and billing indicators together. Text alone is not enough when the product has parallel state surfaces.

## Claim grading

- `【页面/代码事实】`: the claim can be directly pointed to and reproduced.
- `【合理推断】`: multiple facts support it, but alternative implementations remain possible. State the inference chain briefly.
- `【建议设计】`: a proposed mechanism for reliability, safety, quality, or usability.
- `【未知】`: the current evidence does not decide the question.

Use claim-level labels, not a single label for a mixed paragraph.

## Conflict handling

When chat, canvas, task state, asset index, preview, code, or official documentation disagree:

1. record every side with separate evidence IDs;
2. describe the conflict precisely;
3. do not silently privilege the agent's statement;
4. distinguish frontend synchronization issues from confirmed backend state only when evidence permits;
5. add a validation question or recommended single source of truth when appropriate.

## Browser and source inspection

- Maintain the user's readonly boundary.
- Do not click controls that create, regenerate, overwrite, publish, delete, charge, purchase, or send messages.
- Do not inspect credentials or unrelated personal data.
- In source code, cite file paths and line numbers for implementation claims.
- In live UI, capture visible labels, buttons, asset names, status, errors, and chronological position.
- If login or user takeover is required, hand control to the user and wait.

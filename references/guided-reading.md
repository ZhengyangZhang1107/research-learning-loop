# Evidence-Grounded Guided Reading

Use this reference when the learner asks to be led through a paper, wants a concrete explanation, or gets stuck on a figure, equation, sample, or information flow. It is a presentation and diagnosis layer over S2–S5, not a new route, pass, state machine, or note system.

## Prepare the smallest useful evidence packet

Before explaining details, inventory the material already available in the Source Snapshot:

- the exact paper version and supplement;
- searchable text or source with stable section, page, equation, figure, and table locators;
- viewable figure and table assets or direct page access;
- the verified official repository and pinned checkout when code mapping is in scope.

Acquire or materialize missing files only when that write is within the user's scope. An automatically discovered repository is a candidate until an author, project page, or other authoritative source confirms it. If a helper extracts text or crops figures, inspect its output before relying on it; extraction is not evidence that the content was read correctly.

Inspect enough evidence for the current checkpoint to teach rather than narrate a live skim. For a genuine first pass, begin only with metadata and the current S2 anchor; a machine-generated index may be used only to locate that anchor, not to inspect or interpret later headings, captions, references, or results. Advance through the paper in the fixed order instead of privately completing a broad extra pass. For a targeted question, inspect only its anchor and blocking dependencies. Once S2 is complete, S4 may inspect the core method and relevant experiment or appendix sections selectively. If code is in scope, S5 may identify the README command, entrypoint, model path, objective, data transform, and inference or evaluation path. Preserve unavailable material as a gap instead of filling it by guesswork.

Create a compact internal anchor view from existing records:

```text
learning question → paper anchor → figure/table → Claim ID → candidate code anchor
```

This is a derived view. Do not maintain it as another ledger or automatically create a paper note unless the user requests a persistent artifact.

## Keep the fixed first pass and add learner-facing checkpoints

During a genuine first pass, retain the exact S2 order. Use the following checkpoints to decide what the learner should be able to say after each anchor:

| S2 anchor | Learner-facing result |
| --- | --- |
| 标题、摘要 | one-sentence task; concrete input and output; claimed contribution |
| Introduction | problem, prior bottleneck, and the authors' central bet |
| 方法总览图和图注 | how to read the figure; system interface; main information path |
| Method | architecture, objective, data assumptions, and train/inference story at first-pass depth |
| 主实验表 | which Claim the main comparison supports, under which conditions |
| Conclusion / Limitations | claimed scope, admitted cost, assumptions, and failure cases |
| 章节标题和参考文献 | exact anchors for pass 2 and only the prerequisites or citations that may be needed |

Do not turn these results into a second sequence. In `coach` or `pair`, normally present one coherent checkpoint, end with one short retrieval or prediction prompt, and retain a resume pointer. In `execute`, or when the user requests a complete report, checkpoints may be bundled while their boundaries remain visible. If the user jumps directly to a topic, answer it and supply only the minimum missing context; this is not a reordered first pass.

## Concrete explanation protocols

Apply only the protocols that improve the current explanation.

### Figure protocol

1. Inspect the actual image or rendered page. A caption alone does not reveal layout, arrows, colors, or spatial grouping.
2. Display the figure when the interface supports it. Otherwise provide an accessible locator and say that it was not displayed.
3. Begin with orientation: what the figure depicts, reading direction, panels, legend, repeated modules, and visual conventions.
4. State the interface before internals: inputs, outputs, relevant shapes, units, coordinate frames, time window, horizon, or frequency.
5. Follow one important information path and connect it to a Claim or method decision.
6. If the figure is dense, focus on or crop the region currently being explained while preserving the full-figure context.
7. Record the figure, page, and caption anchor. Never describe visual positions that were not inspected.

### Equation protocol

Use this chain for a central equation:

```text
purpose in the method
→ faithful original anchor
→ readable expression
→ symbol / type / shape / unit table
→ one small numerical or geometric instance
→ upstream source and downstream consumer
→ optimization or gradient role when relevant
→ candidate code terms
```

Use notation that renders reliably in the current interface; do not force Unicode or raw LaTeX as a universal rule. If the original layout matters and cannot be rendered faithfully, show the equation image as well. A numerical example illustrates the computation but does not verify the Claim.

### Data specimen protocol

Make at least one sample concrete when data semantics affect understanding:

| Field | Shape and dtype | Unit / frame / range | One value or compact slice | Provenance |
| --- | --- | --- | --- | --- |

Then trace the sample through selection, normalization, augmentation, tokenization, chunking, padding, batching, and any post-processing that matters. Prefer an accessible real sample or published value. Mark generated values as `ILLUSTRATIVE`; never present them as observed data. State when paper and code omit a field or convention.

### Information-flow protocol

Draw the shortest flow that preserves the mechanism. Label each edge or step with relevant shape, type, unit, or coordinate frame, and label operations by frequency:

```text
once per sample | once per rollout | once per layer | once per step | repeated K times
```

Separate training and inference when their inputs, state, gradients, or loops differ. Mark which values are cached, carried to the next step, overwritten, detached, or discarded. For recurrent, autoregressive, optimization-loop, control, or world-model systems, walk at least `t=0` and `t=1` when state evolution is part of the question.

### Concrete paper-to-code walkthrough

Choose one scenario or sample and make each step answer:

```text
what exists now, with a value and shape
→ which paper operation applies
→ which commit:path:symbol implements it
→ what changes
→ what exists next
```

When full dimensions hide the mechanism, first use toy dimensions small enough to enumerate indices, masks, points, rays, tokens, frames, or actions. Label the toy values, then restore the real configuration and state what changes and what remains structurally identical. In `coach` or `pair`, ask the learner to predict one shape, branch, sign, or state update before revealing it. Stop and wait in `coach`; also wait in `pair` when the prediction is the learner-owned part or the learner explicitly requests the gate. Do not reveal or execute past a required gate in the same turn unless the learner waives the pause.

Keep evidence roles explicit: `AUTHOR_CLAIM`, `PAPER_EVIDENCE`, `IMPLEMENTATION_EVIDENCE`, `OBSERVATION`, and `INFERENCE`. If there is no verified code anchor, say so instead of manufacturing a correspondence.

## Repair an explanation that did not land

Do not repeat the same representation with more words. Identify the smallest confusing statement, then try one change at a time:

1. instantiate it with concrete values, units, shapes, geometry, or time;
2. reduce it to toy dimensions and execute each step;
3. contrast it with the simplest plausible alternative and show where that alternative fails;
4. use a physical or everyday analogy, followed immediately by a mapping table back to the paper;
5. if a prerequisite remains, create or refine one S3 Knowledge Bridge Card and return to the original anchor.

After each attempt, ask one diagnostic question that distinguishes understanding from agreement. Update `known` and `blockers`; update `last_verified_step` only after successful recall, and keep `next_action` precise enough to resume a failed attempt. Persist a delivery preference only when the learner states it or the same need recurs; a one-off failure remains a blocker. If the learner restates the idea, begin with `correct`, `partly correct—the gap is ...`, or `not correct—the decisive issue is ...`, then repair only the gap.

## Close and resume cleanly

For a guided checkpoint, finish with:

```text
restateable conclusion:
evidence anchor and current confidence:
resume pointer:
next checkpoint or at most two relevant branches:
```

Do not require a pause after every checkpoint when the requested mode or output favors continuous delivery. Questions and resolved explanations update existing state; they do not automatically create a separate Q&A database. At S8, test the learner with a redraw, prediction, sample trace, or claim-to-evidence link that matches the material just studied.

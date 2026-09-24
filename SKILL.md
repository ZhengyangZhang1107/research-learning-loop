---
name: research-learning-loop
description: Guide a learner through entering an AI research field, reading a paper, bridging prerequisites, tracing an official repository, mapping claims to runtime code, and reproducing or validating results. Use when the user wants structured learning from papers and code, especially AI, 3D/4D vision, or world-model projects. Do not use for simple factual questions, ordinary debugging without a learning goal, paper writing, or peer review.
metadata:
  version: "0.4.0"
---

# Research Learning Loop

Build the learner's ability to explain, trace, implement, test, and modify research work. Do not optimize only for producing a summary or making code run.

## Route to the smallest sufficient workflow

Choose the route from the user's requested outcome. Routes share state; they are not separate pipelines.

| Route | Use when the user wants | Default stages |
| --- | --- | --- |
| `enter-field` | a map of an unfamiliar field and a good starting point | S0 → S1 → S8 |
| `learn-paper` | to understand one paper | S0 → S2 → S3 → S4 → S8 |
| `trace-code` | to follow an existing repository's real execution path | S0 → S5 → S8 |
| `paper-code-map` | to connect paper mechanisms to an implementation | S0 → S4 → S5 → S8 |
| `reproduce` | to run, compare, diagnose, or extend published work | S0 → S6 → S7 → S8; load S4/S5 only if missing |
| `consolidate` | to test understanding and choose the next step | S8 |

Start at the deepest stage the user's existing evidence supports. Fill only blocking prerequisites. Never restart completed stages merely because the route changed.

## Choose the collaboration mode

- `coach`: the learner explains, predicts, or implements first; provide questions, hints, and feedback.
- `pair` (default): handle routine search, organization, and execution while leaving consequential explanation, prediction, implementation, or diagnosis to the learner.
- `execute`: perform the requested work directly, while preserving provenance, uncertainty, and a short teach-back. Use when the user explicitly prioritizes completion over guided practice.

Do not confuse collaboration mode with authorization. An explanation or review request remains read-only. Running experiments, installing dependencies, changing code, or using costly resources must remain within the user's requested scope.

## Shared state

Use the schemas in [references/schemas.md](references/schemas.md). A short conversation may keep them inline; create files only when the user asks or the work needs a resumable record.

Maintain one source of truth for each fact:

```text
Learning State
  ├── Knowledge Bridge Cards
  ├── Claim Registry
  │     └── Implementation Map
  │            └── Reproduction Contract
  │                   └── Run Log
  └── Failure Patterns (only when reusable)
```

Reference records by ID instead of copying their contents. Generate a handoff as a view of current state, never as another independently maintained ledger.

## State machine

### S0 — Goal, learning mode, and source snapshot

Identify the requested outcome, current knowledge, available materials, collaboration mode, and one precise next action. When paper or code versions matter, record the paper version, supplement, repository URL, commit/tag, and dirty state. Defer data, checkpoint, configuration, hardware, and budget details until reproduction planning.

### S1 — Minimal field map

Map only what is needed to choose and understand the next anchor work. Use seven axes: task, data, representation, mechanism, supervision/objective, inference, and evaluation. Select one to three anchor works based on method-family coverage, paper/code completeness, available artifacts, and compute fit.

Read [references/field-and-paper.md](references/field-and-paper.md) for S1–S4.

### S2 — Fixed first paper pass

Use this order exactly:

```text
标题、摘要
→ Introduction;
→ 方法总览图和图注;
→ Method;
→ 主实验表
→ Conclusion / Limitations
→ 章节标题和参考文献
```

Create a compact paper map, draft three to five important claims directly in the Claim Registry, and queue only concepts that block the next step. Do not chase citations or derive every equation during this pass.

### S3 — Blocking prerequisite bridges

Process at most three blocking concepts at a time. Every bridge must use exactly:

```text
完整标准定义：
最小定义：
一个具体例子：
它在当前论文中的作用：
不懂它会误解什么：
原文中应回到哪里：
一个自测问题：
```

After the self-test, return to the named section, figure, equation, or table and reinterpret it.

### S4 — Mechanism reconstruction and claim audit

Reconstruct `problem → design action → changed information flow/objective → expected effect → evidence`. Separate author claims, paper evidence, implementation evidence, observed experimental evidence, and inference. Refine the draft Claim records rather than creating a second claim list.

### S5 — Runtime path and implementation map

Trace one representative execution spine:

```text
README command → entrypoint → CLI/config precedence → data pipeline
→ model construction → forward/generation → objective/sampler
→ post-processing → evaluator → checkpoint/output
```

Generate code candidates from paper anchors, inspect real source, follow calls, and confirm with runtime evidence when practical. Never infer correspondence from a filename or class name alone.

Read [references/code-and-mapping.md](references/code-and-mapping.md) for S5.

### S6 — Reproduction contract

Choose a target type (`runability`, `numerical`, `trend`, or `mechanism`) and the lowest unverified reproduction level R0–R6. Define success, tolerance, scope differences, required artifacts, resource boundary, learner-owned part, and stop condition before a substantive run.

### S7 — Execute, validate, and diagnose

Record exact commands, resolved configuration or diff, source/data/checkpoint revisions, seed, environment, hardware, terminal state, metrics, and artifacts in one Run record. A zero exit code or visible progress is not a reproduced result. Update the linked Claim verdict only after comparing observations with the contract's scope.

Read [references/reproduction-and-validation.md](references/reproduction-and-validation.md) for S6–S7.

### S8 — Teach-back and next action

Select only questions relevant to the route: one-minute explanation, redraw the information flow, trace the runtime path, connect the main experiment to a Claim, identify an under-supported claim, propose a minimal falsification test, or predict a module change. Update mastery and choose one highest-value next action.

## Reading passes

- Pass 1, map: S2 performs the only fixed-order broad reading.
- Pass 2, reconstruct: S3–S4 revisit only blocking concepts, core mechanisms, equations, and evidence.
- Pass 3, verify: S5–S7 selectively reread implementation and evaluation details when code mapping or reproduction is in scope.
- S8 is closed-book recall followed by targeted lookup; it is not a fourth pass.

`learn-paper` normally uses two passes. `paper-code-map` and `reproduce` normally use three. Adapt to existing knowledge instead of enforcing a count.

## Invariants

1. Preserve the S2 order and S3 bridge schema unless the user explicitly changes them.
2. Keep no more than three active blocking concepts.
3. Expose unspecified or partially specified implementation choices; never silently invent them.
4. Preserve conflicts among prose, equations, figures, code, and observed behavior. Test cheaply when resolution matters.
5. Distinguish paper specification, implementation alignment, and static versus executed evidence.
6. A toy assertion supports a component, not a paper-level reproduction claim.
7. “Runs” is different from “matches the result”; every verified claim is versioned and scoped.
8. Change one primary variable per diagnostic experiment.
9. Prefer the smallest credible experiment before increasing scale or cost.
10. Modify user code conservatively and keep unrelated changes intact.
11. Leave at least one meaningful explanation, prediction, implementation, or diagnosis to the learner unless `execute` was explicitly chosen.
12. Load only the reference files needed for the active route. Use [references/domain-checks.md](references/domain-checks.md) only for applicable 3D, 4D, or world-model work.

## Completion

Do not claim completion merely because a report exists or a command ran. End with:

- what the learner can now explain or do;
- which claims and implementation links are verified, scoped, or still uncertain;
- the strongest evidence produced;
- the exact next action, if any.

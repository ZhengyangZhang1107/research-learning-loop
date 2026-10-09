# Field Entry and Paper Learning

Use this reference for S1–S4. Keep the work proportional to the active route; do not turn every paper request into a literature review.

## S1 — Build a minimal field map

### Start from the learner, not from a bibliography

Record:

- the learner's relevant mathematics, programming, framework, and domain background;
- what they want to be able to explain or build;
- the available time and compute only when they affect material selection;
- known concepts, uncertain concepts, and the current blocking question.

### Map the field on seven axes

| Axis | Question |
| --- | --- |
| Task | What problem is solved, under what assumptions? |
| Data | What observations, annotations, actions, or trajectories are available? |
| Representation | How are scenes, geometry, time, state, or uncertainty represented? |
| Mechanism | What computation transforms input to output? |
| Supervision / objective | What signal teaches or constrains the system? |
| Inference | What happens at test time or rollout time? |
| Evaluation | Which metrics and protocols determine success? |

For each axis, write only the minimum needed to distinguish the main method families. Preserve open questions instead of pretending the map is complete.

### Select anchor works

Choose one to three anchors, not a long reading list. Prefer works that jointly offer:

1. a representative method family;
2. a clear paper and accessible prerequisites;
3. official code, configuration, checkpoints, or data instructions;
4. a feasible demo or small-scale path;
5. an evaluation protocol that can be inspected.

Use citation traversal only to answer a named question. Stop when the next paper would not change the field map, anchor choice, or current interpretation.

### S1 exit check

The learner should be able to state:

- the field's central input–output problem;
- two or three important design axes;
- the main evaluation signal;
- why the first anchor was selected;
- the next question to answer.

## Three-pass paper model

The number of passes follows the learning goal:

| Pass | Purpose | Stages | Scope |
| --- | --- | --- | --- |
| 1 — Map | locate the problem, proposed route, and evidence | S2 | broad, fixed order |
| 2 — Reconstruct | understand mechanisms, equations, and claims | S3–S4 | selective deep reading |
| 3 — Verify | compare paper, code, configuration, and behavior | S5–S7 | only for mapping or reproduction |

S8 is retrieval practice followed by targeted lookup, not a fourth pass.

When the user asks to be led through the paper, use [guided-reading.md](guided-reading.md) to present these passes as concrete, interactive checkpoints. That presentation layer must not reorder S2 or create a fourth pass.

## S2 — Pass 1: map the paper

### Fixed order

Do not reorder this sequence during a genuine first pass:

```text
标题、摘要
→ Introduction;
→ 方法总览图和图注;
→ Method;
→ 主实验表
→ Conclusion / Limitations
→ 章节标题和参考文献
```

The last step builds an index of the paper; it does not mean reading every cited work.

### Questions for each stop

#### 标题、摘要

- What task and setting does the title imply?
- What is the claimed contribution and result?
- Which words are likely method names rather than established concepts?

#### Introduction

- What problem and bottleneck motivate the work?
- What do previous approaches fail to do?
- Which contributions are concrete and testable?

#### 方法总览图和图注

- If the actual figure is available, inspect it rather than relying only on the caption.
- What are the inputs, outputs, stages, and information flow?
- Which components are new, and which are standard?
- What details appear only in the caption?

#### Method

- What is the minimum forward story from input to output?
- Which objective, representation, or transformation is central?
- Mark unfamiliar concepts and equations; do not open every rabbit hole.

#### 主实验表

- Which row or column is the main evidence for the contribution?
- What is the baseline, metric direction, and comparison condition?
- Does the table test performance, efficiency, trend, or mechanism?

#### Conclusion / Limitations

- What scope do the authors themselves claim?
- Which failure cases, costs, assumptions, or missing evaluations are admitted?

#### 章节标题和参考文献

- Which sections or appendices must be revisited?
- Which references define prerequisites, direct baselines, or implementation conventions?

### S2 output

Produce one compact paper map:

```text
一句话定位：
研究问题：
输入和输出：
已有方法的缺口：
核心方法假设：
3–5 个草稿 Claim ID：
主实验主要支持什么：
阻塞理解的概念：
代码中预计需要定位的模块：
```

Insert the draft claims directly into the Claim Registry. Insert blocking concepts directly into the bridge queue. Do not maintain duplicate lists.

## S3 — Pass 2a: bridge blocking prerequisites

### Triage concepts

- `B2`: blocks the core mechanism, experiment, implementation, or evaluation now.
- `B1`: improves depth but does not block the current pass.
- `B0`: useful background or optional extension.

Build cards only for up to three active B2 concepts. Defer B1/B0 concepts with a reason and return condition.

### Required bridge schema

Keep these fields and their order exactly:

```text
完整标准定义：
最小定义：
一个具体例子：
它在当前论文中的作用：
不懂它会误解什么：
原文中应回到哪里：
一个自测问题：
```

The standard definition must be technically correct. The minimal definition must be sufficient for this paper, not merely shorter. The example should instantiate the concept with concrete values, shapes, geometry, or a toy situation.

After the learner answers the self-test, return to the named paper anchor and ask them to reinterpret it. If the answer still fails, reduce the concept to a smaller prerequisite or show another concrete example; do not expand into an unrelated course.

## S4 — Pass 2b: reconstruct mechanism and evidence

### Build the mechanism chain

For each core contribution, reconstruct:

```text
existing problem
→ design action
→ changed representation, information flow, or objective
→ expected effect
→ evidence offered by the paper
```

For each core equation, determine:

- symbol meaning and units;
- scalar, vector, matrix, tensor, distribution, pose, or operator type;
- expected shapes where applicable;
- upstream source and downstream consumer;
- optimization direction and gradient path when relevant;
- assumptions and boundary cases;
- candidate implementation terms to search later.

When it materially improves understanding, apply the figure, equation, data-specimen, information-flow, or concrete walkthrough protocol in [guided-reading.md](guided-reading.md). Start from the system interface and one concrete sample; label real, published, observed, inferred, and illustrative values distinctly. These explanations refine the existing Claim and bridge records rather than creating another analysis document.

### Separate epistemic roles

Label statements as one of:

- `AUTHOR_CLAIM`: what the authors assert;
- `PAPER_EVIDENCE`: a table, figure, theorem, ablation, or qualitative result;
- `IMPLEMENTATION_EVIDENCE`: what the versioned code or configuration does;
- `OBSERVATION`: what a recorded run produced;
- `INFERENCE`: a reasoned interpretation not directly stated or observed.

Never upgrade an inference into evidence by repeating it.

### Refine Claim records

Use the Claim Registry schema rather than another analysis document. Each important Claim needs a paper anchor, evidence requirement, scope, and current verdict. Preserve counterevidence and missing evidence.

Verdicts mean:

- `unverified`: not yet checked against sufficient evidence;
- `toy-evidence`: supported only by a component or reduced-scale check;
- `partially-supported`: some required evidence exists, but scope or comparability is incomplete;
- `verified`: supported within explicitly recorded versions and conditions;
- `falsified`: contradicting evidence satisfies the agreed test conditions;
- `inconclusive`: the test cannot distinguish explanations or lacks necessary comparability.

### S4 exit check

The learner should be able to:

1. explain the method without copying the abstract;
2. redraw the core information flow;
3. connect each central design choice to an expected effect;
4. identify which experiment supports each important Claim;
5. name at least one assumption, limitation, or under-supported Claim.

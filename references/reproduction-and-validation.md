# Reproduction and Validation

Use this reference for S6–S7. Validation is a scoped test of a versioned Claim and/or implementation decision, not a binary label attached to an entire paper or repository.

## S6 — Define the reproduction contract

### Choose the target type

- `runability`: the documented artifact runs under recorded conditions;
- `numerical`: a metric or value falls within an agreed tolerance;
- `trend`: a ranking, curve direction, or ablation trend is preserved;
- `mechanism`: a targeted intervention supports the proposed causal or functional explanation.

### Choose the reproduction level

```text
C0  Isolated component or mechanism micro-test; scoped evidence, not an end-to-end reproduction level
R0  Environment and dependencies are usable
R1  Official sample or demo runs
R2  Official checkpoint inference runs
R3  Official evaluation path produces comparable metrics
R4  Single-sample or tiny training completes end to end
R5  Official-scale result is matched within the contract
R6  One-variable ablation, modification, or falsification test
```

Use C0 for a hypothesis-driven or interventional shape, unit, gradient, branch, transform, or state-transition check with a predeclared pass criterion. A purely observational execution with no pass criterion is a trace Run, not C0. Begin end-to-end reproduction at the lowest R level not already supported by trustworthy evidence. One Contract selects one level; when C0 precedes or accompanies an R level, create separate Contracts and linked Runs. C0 never upgrades an end-to-end level by itself. Do not force a rerun of lower levels when their artifacts, versions, and conditions are already adequate.

### Define success before execution

Create one Reproduction Contract containing:

- at least one linked Claim ID or Implementation ID;
- target type and target level;
- paper, code, or specification conditions versus current conditions;
- pass criterion and tolerance basis;
- required logs, metrics, checkpoints, predictions, or plots;
- time, compute, storage, and cost boundary;
- the part the learner will explain, implement, predict, or diagnose;
- stop and failure conditions.

Do not choose tolerance after seeing the result unless the change is explicitly recorded and justified.

### Record scope delta once

Compare only dimensions relevant to the target:

```text
dataset and split
preprocessing
model and parameter scale
checkpoint
training steps or epochs
optimizer and schedule
hardware and precision
evaluation sample count
metric implementation
number of seeds
wall time and cost
```

Keep this comparison in the Reproduction Contract. Runs reference the contract and record only overrides.

## Conditional preflight

Run only checks that can retire a meaningful risk:

- exact-shape and dtype micro-test for an uncertain third-party API;
- CPU or tiny end-to-end path;
- preprocessing, units, color range, and metric sanity checks;
- checkpoint load/save/resume check when training continuity matters;
- GPU memory, storage, wall-time, and cost estimate;
- immutable baseline command, configuration, and output;
- data access, license, or authentication availability.

If a check cannot change the plan, omit it.

## S7 — Execute through one reproduction Run lifecycle

Use one record with `run_purpose: reproduction` and the Contract ID from planning through termination:

```text
planned → running → completed / failed / cancelled
```

Record the exact command and resolved configuration or diff, not only the config filename. Capture data and checkpoint revisions, seed, environment, hardware, start/end or duration, terminal state, metrics, and artifact locations.

A run is not complete merely because:

- the process started;
- a job was submitted;
- the progress bar reached an intermediate step;
- the command returned exit code zero;
- an output file exists.

Completion requires the terminal evidence and artifacts named in the contract.

## Interpret the run

A reproduction Run outcome is only:

- `pass`: it met this contract's criterion;
- `fail`: it violated the criterion under comparable conditions;
- `inconclusive`: missing comparability, weak power, ambiguous failure, or insufficient evidence prevents judgment.

For a Claim-targeting Contract, aggregate linked Runs into the Claim verdict; one passing toy run normally produces `toy-evidence`, not `verified`. For an implementation-only C0 Contract, update the Implementation Map's alignment, evidence level, relation basis, and confidence within the tested scope; do not create or change a Claim verdict merely to hold the result.

Use language proportional to evidence:

- “The component assertion passed at toy dimensions.”
- “The trend was preserved on the recorded subset.”
- “The official metric was reproduced within tolerance under these conditions.”
- Never replace these with the broader statement “the paper was reproduced” unless the contract genuinely supports it.

## Diagnose discrepancies in a high-yield order

Check:

1. units, scale, normalization, color range, and metric direction;
2. sign, loss weighting, reduction, and optimization direction;
3. mask, padding, indexing, shape broadcasting, and coordinate frame;
4. configuration precedence, inactive branches, and runtime mutation;
5. dataset version, split, filtering, and preprocessing;
6. checkpoint variant and load coverage;
7. evaluation implementation and post-processing;
8. seed and nondeterminism;
9. batch size, training duration, model scale, and hardware precision;
10. an independent rerun after a concrete hypothesis is formed.

Change one primary variable per diagnostic run. Preserve the last trustworthy baseline.

## Patch conservatively

When a fix is required:

- make the smallest change that tests the hypothesis;
- keep paper-faithful behavior distinguishable from compatibility or engineering patches;
- record the diff or override in the Run;
- do not clean up unrelated code;
- rerun the smallest relevant test before returning to the target run.

## Promote only reusable failures

Keep an ordinary failure in its Run. Create a Failure Pattern only when the root cause is confirmed and reusable, the same signature recurs, or the risk is high enough to justify prevention.

Promote its prevention check into preflight only when that check is cheap, discriminating, and likely to recur. Do not accumulate project-specific folklore as universal rules.

## S7 exit check

Before concluding, answer:

- What exact Claim and/or Implementation decision, target level, and scope were tested?
- Which source, code, data, checkpoint, config, and hardware versions were used?
- What was expected and observed?
- Did the Run pass, fail, or remain inconclusive?
- What evidence changes the Implementation Map and, if linked, the Claim verdict?
- What is the smallest justified next action?

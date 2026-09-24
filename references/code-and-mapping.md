# Code Tracing and Paper–Code Mapping

Use this reference for S5. The goal is to understand the runtime implementation of a named mechanism or claim, not to summarize every directory.

## Freeze the code source

Before making a durable mapping, record the repository URL, commit or tag, and dirty state in the Learning State's Source Snapshot. If the paper, released code, checkpoint, or configuration comes from different dates, preserve that drift rather than treating them as one version.

## Build a minimal repository route

Inspect only enough structure to identify:

- documented commands and supported tasks;
- entrypoints;
- configuration locations;
- data, model, objective, evaluation, and output modules;
- external or generated components that are not in the repository.

Do not create a complete file-by-file inventory unless the repository architecture itself is the learning target.

## Trace one representative execution spine

Start from a command that is meant to run:

```text
README command
→ shell or Python entrypoint
→ argument parsing
→ configuration loading, defaults, and overrides
→ dataset and preprocessing
→ model/component construction
→ forward, generation, or rollout
→ loss, objective, sampler, or controller
→ post-processing
→ evaluator and metric implementation
→ checkpoint, visualization, or output artifact
```

Follow one sample or batch end to end. Record important types, tensor shapes, coordinate frames, units, device/dtype changes, and branching configuration values.

## Locate code from paper anchors

Use a candidate-confirmation process:

1. Extract anchors from the paper: component names, equation symbols, loss terms, hyperparameters, algorithm steps, or figure labels.
2. Generate search candidates, including synonyms and likely configuration keys.
3. Search definitions, imports, call sites, registries, factories, and configuration references.
4. Read the actual source around each candidate.
5. Follow callers and callees until the candidate is connected to the representative execution spine.
6. Confirm with a breakpoint, hook, trace, log, or tiny execution when practical.
7. Downgrade confidence if dispatch is dynamic, the path is inactive, or only naming similarity exists.

A filename, class name, comment, or README statement is a clue, not proof.

## Resolve effective configuration

Determine precedence rather than listing every config file. Check, as applicable:

```text
library default
< base configuration
< experiment configuration
< checkpoint metadata
< environment variable
< CLI override
< runtime mutation
```

Record only keys that affect the target mechanism, data path, metric, or reproduction condition. If precedence is uncertain, create a tiny run that prints or asserts the resolved value.

## Maintain the Implementation Map

Use one Implementation Map for both ambiguity auditing and paper–code correspondence. Do not create a separate ambiguity table.

Three dimensions must remain independent:

### Paper specification status

- `specified`: the paper or supplement explicitly states the detail;
- `partial`: it constrains the choice but leaves ambiguity;
- `unspecified`: it does not state the implementation-relevant choice.

### Implementation alignment

- `match`: observed implementation agrees within the recorded scope;
- `partial`: only part of the described mechanism is present or comparable;
- `conflict`: paper and implementation differ materially;
- `not-found`: no confirmed active implementation has been located.

### Evidence level

- `static`: supported by source/config inspection only;
- `executed`: observed on the active runtime path.

Do not convert `unspecified` into `specified` merely because official code makes a choice. Record the choice as implementation evidence. Official code can clarify behavior but cannot prove the paper originally specified or intended it.

## Component validation ladder

For important components, try to form:

```text
paper anchor
→ code anchor at commit:path:symbol
→ concrete input
→ intermediate shapes and selected values
→ output
→ toy assertion
```

Applicable checks include:

- input/output and intermediate shapes;
- finite values and expected ranges;
- units and normalization;
- mask, padding, and indexing behavior;
- coordinate transforms and inverse consistency;
- gradient existence and direction;
- degenerate or boundary inputs;
- configuration switches activating the expected branch;
- deterministic behavior under a fixed seed where expected.

These checks validate components. They do not by themselves verify a paper-level Claim.

## Handle conflicts

When prose, equation, figure, appendix, configuration, code, and runtime behavior disagree:

1. record every source and its version;
2. state the exact conflict without silently choosing a winner;
3. assess whether it changes the target Claim or reproduction result;
4. use a minimal A/B or micro-test when cheap and discriminating;
5. otherwise leave the mapping `partial`, `conflict`, or `inconclusive`.

## S5 exit check

The learner should be able to:

- start from the documented command and point to the real entrypoint;
- explain where the target data, model, objective, and metric flow;
- identify the effective configuration values and their precedence;
- locate the core paper mechanism at `commit:path:symbol`;
- distinguish static candidates from code actually reached at runtime;
- name one unresolved ambiguity or paper–code mismatch.

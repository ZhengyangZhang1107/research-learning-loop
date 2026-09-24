# Shared Schemas

These schemas are the single sources of truth for resumable work. Instantiate only the records required by the active route. For a short task, render them inline instead of creating files.

Use stable IDs such as `C-01`, `I-01`, `RC-01`, `RUN-001`, and `FP-01`. Reference another record by ID rather than copying its content.

## Learning State

```yaml
learning_state:
  goal: ""
  requested_output: ""
  route: enter-field | learn-paper | trace-code | paper-code-map | reproduce | consolidate
  collaboration_mode: coach | pair | execute
  current_stage: S0 | S1 | S2 | S3 | S4 | S5 | S6 | S7 | S8
  known: []
  blockers: []
  deferred: []
  mastery:
    field: L0 | L1 | L2 | L3 | L4 | L5
    paper: L0 | L1 | L2 | L3 | L4 | L5
    code: L0 | L1 | L2 | L3 | L4 | L5
    reproduction: L0 | L1 | L2 | L3 | L4 | L5
  source_snapshot:
    snapshot_id: SS-01
    paper_version: ""
    supplement_version: ""
    repository_url: ""
    commit_or_tag: ""
    dirty_state: ""
  field_map:
    task: ""
    data: ""
    representation: ""
    mechanism: ""
    supervision_or_objective: ""
    inference: ""
    evaluation: ""
  search_record:             # Only when enter-field actually searches.
    queries: []
    selection_reasons: []
    exclusion_reasons: []
  last_verified_step: ""
  next_action: ""
```

Mastery levels:

- `L0`: encountered;
- `L1`: can give a minimal definition or problem statement;
- `L2`: can reconstruct the core mechanism;
- `L3`: can trace the runtime implementation;
- `L4`: can reproduce and diagnose discrepancies;
- `L5`: can modify the method, predict consequences, and validate them.

## Knowledge Bridge Card

Do not rename or reorder these fields.

```text
bridge_id：
concept：
level：B2 / B1 / B0

完整标准定义：
最小定义：
一个具体例子：
它在当前论文中的作用：
不懂它会误解什么：
原文中应回到哪里：
一个自测问题：

self_test_result：
remaining_confusion：
```

Only `B2` cards are active by default. `B1` and `B0` remain deferred until the route needs them.

## Claim Registry

```yaml
claim:
  claim_id: C-01
  claim_text: ""
  claim_type: mechanism | performance | efficiency | theory | qualitative
  paper_anchor: "section / equation / figure / table / appendix"
  paper_evidence: []
  potential_counterevidence: []
  required_evidence: []
  scope: ""
  verdict: unverified | toy-evidence | partially-supported | verified | falsified | inconclusive
  linked_implementation_ids: []
  linked_run_ids: []
```

The Claim Registry owns the aggregate verdict. Do not duplicate detailed code paths or raw run observations here.

## Implementation Map

This record combines implementation ambiguity and paper–code mapping.

```yaml
implementation:
  implementation_id: I-01
  component_or_decision: ""
  linked_claim_ids: []
  paper_anchor: ""
  specification_status: specified | partial | unspecified
  expected_behavior: ""
  code_anchor: "commit:path:symbol or not-found"
  call_path: []
  effective_config_and_precedence: []
  current_choice: ""
  alternatives: []
  risk_if_wrong: ""
  alignment: match | partial | conflict | not-found
  evidence_level: static | executed
  relation_basis: extracted | runtime-confirmed | inferred | ambiguous
  confidence: high | medium | low
  linked_run_ids: []
```

`relation_basis` describes how the paper–code relation was established:

- `extracted`: directly supported by paper/code names, comments, or documentation but not executed;
- `runtime-confirmed`: reached on the recorded active path;
- `inferred`: reasoned correspondence with incomplete direct support;
- `ambiguous`: multiple plausible mappings remain.

## Reproduction Contract

```yaml
reproduction_contract:
  contract_id: RC-01
  target_claim_ids: []
  reproduction_type: runability | numerical | trend | mechanism
  target_level: R0 | R1 | R2 | R3 | R4 | R5 | R6
  repo_readiness:              # Fill only relevant entries.
    dependencies: available | partial | missing | unknown
    training_code: available | partial | missing | not-needed | unknown
    evaluation_code: available | partial | missing | not-needed | unknown
    pretrained_assets: available | partial | missing | not-needed | unknown
    exact_result_command: available | partial | missing | unknown
  scope_delta:
    paper_conditions: {}
    current_conditions: {}
    material_differences: []
  pass_criterion: ""
  tolerance_and_basis: ""
  required_artifacts: []
  budget:
    wall_time: ""
    compute: ""
    storage: ""
    monetary_cost: ""
  learner_owned_part: ""
  stop_or_failure_condition: ""
```

The Contract owns success criteria and scope differences. Do not restate them in every Run.

## Run Log

Use one record from planning through termination.

```yaml
run:
  run_id: RUN-001
  lifecycle: planned | running | completed | failed | cancelled
  contract_id: RC-01
  linked_claim_ids: []
  linked_implementation_ids: []
  hypothesis: ""
  baseline_run_id: ""
  one_changed_variable: ""
  source_snapshot_ref: ""
  source_overrides: []
  exact_command: ""
  resolved_config_or_diff: ""
  data_revision: ""
  checkpoint_revision: ""
  seed: ""
  environment: ""
  hardware: ""
  expected_result: ""
  terminal_state: ""
  observed_metrics: {}
  artifacts: []
  test_outcome: pass | fail | inconclusive
  interpretation: ""
  failure_diagnosis:
    symptom: ""
    impact: ""
    root_cause_status: unknown | suspected | confirmed
    evidence: []
    fix: ""
    prevention_candidate: ""
```

The Run owns raw observations. The Claim Registry owns the cross-run verdict.

## Failure Pattern

Create only for a confirmed, recurring, or high-risk reusable failure.

```yaml
failure_pattern:
  failure_pattern_id: FP-01
  source_run_ids: []
  signature: ""
  root_cause_status: suspected | confirmed
  diagnosis_evidence: []
  fix: ""
  prevention_check: ""
  status: open | resolved
```

## Derived handoff view

Generate this from the current records. Never maintain it independently.

```text
当前目标、路线和阶段：
Source Snapshot：
开放的 Claim / Implementation ID：
最后一个可信 Run ID：
当前 Failure Pattern 或阻塞项：
用户已经能够独立完成什么：
下一项精确动作：
```

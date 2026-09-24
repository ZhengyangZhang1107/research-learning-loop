# Design Provenance

This project synthesizes methods from open-source research, tutoring, code-navigation, and reproducibility projects. The workflow and wording in this repository are newly organized for a learner-centered paper–code–reproduction loop; source code and templates were not copied.

Star counts below are approximate GitHub API snapshots from 2026-09-24 and will change. Popularity was used as one signal for mature design, not as a proxy for methodological correctness.

## High-star architectural references

| Project | Snapshot / license | Design influence | Deliberately not adopted |
| --- | --- | --- | --- |
| [Graphify](https://github.com/Graphify-Labs/graphify) | ≈121k / Apache-2.0 | Explicitly label extracted versus inferred relations; this project extends the distinction with ambiguous and runtime-confirmed states | Persistent knowledge graph, Wiki, or Obsidian dependency |
| [Aider](https://github.com/Aider-AI/aider) and its [repository map](https://github.com/Aider-AI/aider/blob/main/aider/website/docs/repomap.md) | ≈49.1k / Apache-2.0 | Compact file/symbol map ranked by relevance and dependency | Treating a repository map as runtime or behavioral evidence |
| [K-Dense scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) | ≈46.4k / MIT | Search-query recording, screening, deduplication, and source verification | Turning ordinary field entry into a mandatory systematic review |
| [DeepTutor](https://github.com/HKUDS/DeepTutor) | ≈40.2k / Apache-2.0 | Multiple learning modes sharing learner state and recoverable progress | Heavy RAG, knowledge-base, and application runtime |
| [Agent Skills specification](https://github.com/agentskills/agentskills/blob/main/docs/specification.mdx) | ≈25.6k / Apache-2.0 | `SKILL.md`, progressive disclosure, and optional references/scripts/assets | Empty resource folders or scripts without a demonstrated need |
| [Hugging Face Skills](https://github.com/huggingface/skills) | ≈11.1k / Apache-2.0 | Optional discovery of paper metadata and linked models, datasets, Spaces, and repositories | Hard dependency on Hugging Face services |
| [PaperQA2](https://github.com/Future-House/paper-qa) | ≈9.2k / Apache-2.0 | Candidate retrieval, query-conditioned evidence selection, and citation-grounded answers | Replacing close paper reading with chunk retrieval |
| [Paper2Code](https://github.com/going-doer/Paper2Code) | ≈5.0k / Apache-2.0 | Separating design recovery from implementation | Default generation of a complete implementation |
| [Papers with Code: releasing research code](https://github.com/paperswithcode/releasing-research-code) | ≈3.0k / MIT | Repository readiness: dependencies, training, evaluation, pretrained assets, and exact result commands | A separate completeness document for every task |
| [paper2code](https://github.com/PrathamLearnsToCode/paper2code) | ≈1.5k / MIT | `SPECIFIED / PARTIALLY_SPECIFIED / UNSPECIFIED`, citation anchors, and paper → code → toy assertion | Mandatory auto-generation, silent defaults, or treating a toy test as reproduction |
| [OpenAI Frontier Evals / PaperBench](https://github.com/openai/frontier-evals/tree/main/project/paperbench) | ≈1.3k / MIT | Claim-oriented reproduction evaluation and explicit evidence expectations | Benchmark infrastructure unrelated to the learner's project |

## Specialized methodological references

These repositories have smaller audiences but contain narrow methods useful to this workflow.

| Project | License/status | Design influence | Deliberately not adopted |
| --- | --- | --- | --- |
| [RigorPilot](https://github.com/lllllllama/RigorPilot-Skills/blob/main/skills/ai-research-reproduction/SKILL.md) | MIT | Minimal trustworthy target, conservative patch boundary, and “runs” versus “matches” | Skipping implementation reading when the learner's goal is code understanding |
| [UCL paper–code auditor](https://github.com/UCL-ERL/skills/blob/main/skills/evaluation/paper-code-consistency-auditor/SKILL.md) | MIT | Version contract, effective configuration, and paper/code drift | A second audit report duplicating the Implementation Map |
| [UCL provenance auditor](https://github.com/UCL-ERL/skills/blob/main/skills/evaluation/experiment-provenance-auditor/SKILL.md) | MIT | Commit, config, data, seed, hardware, command, log, checkpoint, and artifact provenance | A separate provenance ledger duplicating Run records |
| [paper-reading-coach](https://github.com/ITerminaTor996/paper-reading-coach-skill/blob/main/paper-reading-coach/SKILL.md) | MIT | Questions at high-value understanding gates and active recall | Replacing the user's fixed first-pass order |
| [techdou/paper-reading](https://github.com/techdou/paper-reading/blob/main/SKILL.md) | Apache-2.0 | Problem → bottleneck → design → information-flow change → evidence → scoped conclusion | Its paper-order conventions where they conflict with this project |
| [HF paper-reproduction](https://huggingface.co/rogermt/nsgf-plusplus/blob/main/SKILL.md) | Community Skill | Exact-shape API micro-tests, tiny end-to-end runs, resource estimates, and checkpoint/resume checks | Domain-specific Sinkhorn, UNet, or hosted-notebook rules |
| [ICML 2026 Open Reproductions](https://huggingface.co/datasets/ICML-2026-agent-repro/challenge/blob/main/README.md) | MIT dataset repository | Claim-by-claim evidence, exact commit/command/artifact capture, scope and cost delta, and inconclusive outcomes | Requiring a particular experiment service or one web page per claim |

## Public ideas from repositories without a detected license

The following were used only to cross-check public ideas. No wording, template, or code was copied:

- [research-paper-code-study-codex-skill](https://github.com/baizhanxu/research-paper-code-study-codex-skill): mode routing and following a real runtime path.
- [paper2code-qa](https://github.com/Hoemr/paper2code-qa): generate candidates from paper anchors, then confirm or downgrade them by reading source and call paths.

## Resulting synthesis

The main original integration in this repository is:

```text
field entry
→ fixed first paper pass
→ blocking knowledge bridges
→ mechanism and Claim reconstruction
→ versioned runtime tracing
→ unified implementation/ambiguity mapping
→ scoped reproduction contract
→ provenance-complete Runs
→ active recall and ability progression
```

Redundancy is controlled by keeping one owner for each fact: Claim Registry for aggregate claims, Implementation Map for code relations, Reproduction Contract for success and scope, Run Log for observations, and Failure Patterns only for reusable diagnosed failures.

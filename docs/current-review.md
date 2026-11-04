# Current review guide

This guide describes the reader-facing scope of the November 3, 2026 navigation draft. It preserves the research files at [audit commit 4e5d742](https://github.com/node-and-norm/applied-ai-research-translator/tree/4e5d742378dd2fecbafd525eeb9754c975b83aa0). The [prior README](../README-2026-11-03.md) remains available in full.

## Method and implementation

The specification proposes source classification, claim extraction, bounded tasks, evaluation and human decisions. The repository implements these steps across several paths. Read the [translation method](../TRANSLATION-METHOD.md) alongside the code that executes the intended path.

| Path | Implemented behavior | Boundary |
| :--- | :--- | :--- |
| Model runloop | Collects accept, override or reject through an interactive prompt. [Gate](../runloop/src/human_gate.py) | Empty notes and unrestricted override text can pass. The prompt's request for a rationale exceeds its enforced checks. [Gate code](../runloop/src/human_gate.py) |
| Deterministic example runner | Reads supplied inputs and writes output and decision-summary artifacts. [Runner](../src/runner/run_task.py) | This path has no interactive human-gate prompt. [Runner code](../src/runner/run_task.py) |
| Summary assembly | Uses predefined summary text in addition to run artifacts. [Assembler](../runloop/make_decision_summary.py), [second assembler](../runloop/make_decision_summary_t_c04.py) | Fixed confidence, benefit and sign-off text needs independent support before use as a measured outcome. [Assembler text](../runloop/make_decision_summary_t_c04.py) |
| Saved run artifacts | The logger writes files under an identifier. [Logger](../runloop/src/logger.py) | Reusing a path can replace existing files. Preserve outputs separately when an immutable research record is needed. [Write behavior](../runloop/src/logger.py) |

## Source and result limits

A source pack is an editorial translation of source material. Schema checks establish its declared structure. They leave source accuracy, evidential fit and institutional relevance to substantive review. [Limitations register](../LIMITATIONS.md).

Several retained artifacts need closer review before they support stronger claims:

- The reliance pack contains placeholder evidence quotations. Passage-level provenance remains incomplete. [Claims](../packs/haic_reliance_review_59e257ff/claims.json)
- The production-measurement pack has empty dataset, metric and grader lists in its evaluation plan. [Plan](../packs/measuring_agents_in_production_a98e2ca8/eval_plan.json)
- The multi-agent pack retains a rejection summary alongside a later intake route for review and policy mapping. These describe different artifacts and need joint interpretation. [Summary](../packs/multi_agent_failure_modes_e0228882/decision_summary.json), [intake](../packs/multi_agent_failure_modes_e0228882/safety_policy_intake.json)
- Demo C's manifest records unanimous abstention, while the scenario prose describes disagreement. The committed collection holds summaries and manifests. Raw run artifacts would be needed to reconstruct the execution. [Manifest](demo-runs/C/run-manifest.json), [scenario account](demo-runs/LOCKED_3_DEMO_RUNS.md), [collection](demo-runs/)
- The human-influence pack proposes an assessment approach with an evaluation-only boundary. It supplies research lineage for HIT. [Pack status](../packs/gradual_disempowerment_human_influence_2501a/README.md)

The workflow validates intake files and tolerates failure in two pack-validation calls. Its success therefore needs interpretation at the job-step level. [Workflow](../.github/workflows/validate-artifacts.yml). The [bounded verification guide](reference-verification.md) runs the named checks directly.

## AI roles and human verification

The historical disclosure identifies AI assistance in research, drafting, schema design, code and governance language. It assigns responsibility to the author. The disclosure also recognizes source dependence and limits of human review. [Limitations and AI disclosure](../LIMITATIONS.md).

Codex prepared the current presentation and verification instructions from these repository artifacts. This work records implementation boundaries. It supplies no new source-original review, human performance measurement or independent validation of the method. [Review objects](../LIMITATIONS.md), [source artifacts](../packs/).

## Citation boundary

[CITATION.cff](../CITATION.cff) records version 1.1.1, June 1, 2026 and DOI `10.5281/zenodo.20478121`. The [prior README](../README-2026-11-03.md) links `10.5281/zenodo.20478120`. This presentation uses the existing CFF identity and preserves the earlier link. The relationship between those identifiers requires metadata reconciliation before a claim about their roles is made.

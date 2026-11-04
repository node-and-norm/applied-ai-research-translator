# Bounded verification

Run these checks from a fresh disposable checkout. They validate selected record structures and generate example artifacts. The commands follow the existing [validators](../scripts/) and [example runner](../scripts/run_examples.sh).

## Environment

Use Python 3.11, the version declared by the [workflow](../.github/workflows/validate-artifacts.yml), and `jsonschema==4.23.0` from [requirements.txt](../requirements.txt). The local checks below need no model account or provider credentials.

```sh
python3.11 -m venv .venv
. .venv/bin/activate
python -m pip install -r requirements.txt
```

The environment directory is local setup. Installation requires access to the package registry. The declared dependency version remains unchanged. [Requirements](../requirements.txt).

## Validate a selected pack

The first three scripts accept a pack directory. The decision-summary script accepts a JSON file. [Pack validator](../scripts/validate_pack.sh), [claim validator](../scripts/validate_claims.sh), [task validator](../scripts/validate_tasks.sh), [summary validator](../scripts/validate_decision_summary.sh).

```sh
bash scripts/validate_pack.sh packs/haic_reliance_review_59e257ff
bash scripts/validate_claims.sh packs/haic_reliance_review_59e257ff
bash scripts/validate_tasks.sh packs/haic_reliance_review_59e257ff
bash scripts/validate_decision_summary.sh packs/haic_reliance_review_59e257ff/decision_summary.json
```

Expected output: each command exits zero and reports that its named JSON artifact validates against the corresponding schema. These commands check structure. Source quotations and substantive judgments need the [review described separately](current-review.md).

## Run deterministic examples

The example script invokes the repository's deterministic runner and validators. Its inputs are committed examples. [Script](../scripts/run_examples.sh), [input files](../examples/runs/).

```sh
bash scripts/run_examples.sh
```

Expected output: both example tasks complete, their output and summary validators pass, and the final line reports `All examples ran + validated`. The script writes these directories:

```text
runs/example_t_c02_from_examples/
runs/example_t_c04_from_examples/
```

Run the examples in a disposable copy because repeated identifiers reuse output paths. The resulting artifacts establish behavior on the supplied inputs. They provide no measurement of model performance, human review quality or institutional benefit. [Runner](../src/runner/run_task.py), [limits](../LIMITATIONS.md).

## Model execution and research review

Model execution has separate inputs, configuration and human-review requirements. Follow the [preserved technical instructions](../README-2026-11-03.md) alongside the [runloop code](../runloop/), and verify its arguments before execution. This guide authorizes no live model run. The [implementation review](current-review.md#method-and-implementation) describes the enforced gate and remaining gaps.

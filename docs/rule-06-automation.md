# Rule 6: Automate repeated steps into scripted workflows

## Minimum automation principle

Manual execution is acceptable while a project step is still exploratory. Once a step is repeated or becomes a part of the intended analysis, it should become a script. When several scripts depend on one another, the project needs a workflow. At minimum, the workflow should clarify what the inputs and outputs are, what can be overwritten, what can be regenerated, and where logs are stored.

This principle applies whether the workflow is local, server-based, or run on a cluster. For a small behavioral project, a single command may run multiple steps, such as ingestion, preprocessing, merging, quality-control reporting, and export in order. A larger neuroimaging, electrophysiology, or modeling workflow requires wrappers or workflow managers that coordinate several tools and preserve logs, working directories, and outputs.

Not all steps benefit equally from automation at the same stage of a project. The list below reflects a rough priority order: steps that run frequently, produce large numbers of output files, or feed directly into downstream scripts should be automated first, since manual execution of those steps is most likely to introduce path errors or silent inconsistencies.

## What to automate first

- Data extraction or synchronization
- File unpacking and restructuring
- Preprocessing
- Event-file construction
- Group-level merging
- QC report generation
- Model fitting
- Figure/report generation
- Export or archival step

## Minimal wrapper script with logging and error handling

A wrapper script does not perform the analysis itself; it calls the scripts that do, in the right order, with explicit paths and error handling.

```bash
#!/usr/bin/env bash
set -euo pipefail

PROJECT_ROOT="/path/to/project"
LOG_DIR="${PROJECT_ROOT}/logs"
mkdir -p "$LOG_DIR"

echo "[$(date)] Starting step"

# Example command
python scripts/preprocess_individual.py \
  --input data/raw \
  --output data/processed

echo "[$(date)] Finished step"
```

## Example workflow layout

```text
scripts/
├── 00_extract_data.sh
├── 01_structure_data.py
├── 02_preprocess_individual.py
├── 03_merge_group_level.py
├── 04_qc_report.py
├── 05_run_models.sh
└── 06_export_outputs.py
```

DVC can be used both to version large data files and to define simple workflow stages. In Rule 2, DVC was introduced as a way to link large data or generated outputs to specific code states. Here, the same tool is used to record how analysis steps depend on one another. A DVC stage specifies a command, its dependencies, and its outputs. When an input or script changes, DVC can identify which outputs are stale and rerun the affected stages. This makes DVC useful for small-to-medium workflows that need both data tracking and executable step dependencies.

## Example DVC stage pattern

```yaml
stages:
  preprocess:
    cmd: python scripts/preprocess_individual.py
    deps:
      - scripts/preprocess_individual.py
      - data/raw
    outs:
      - data/processed

  qc:
    cmd: python scripts/qc_missed_keys_report.py
    deps:
      - scripts/qc_missed_keys_report.py
      - data/processed
    outs:
      - qc/missed_keys_report.pdf
      - qc/missed_keys_master.csv
```

## Running the workflow

```bash
dvc repro
```

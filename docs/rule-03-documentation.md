# Rule 3: Document as you build

## What a good README should contain

```markdown
# Project title

## Purpose
Briefly describe the scientific or analytical goal.

## Inputs
List required data inputs and where they should be located.

## Outputs
List generated outputs and where they are written.

## How to run
Give the minimum command sequence needed to reproduce the main workflow.

## Project structure
Explain the main folders: data, scripts, notebooks, reports, figures, docs.

## Environment
State how to recreate the computational environment.

## Reproducibility notes
Mention version control, data versioning, assumptions, and known limitations.
```

## Example `/docs` structure

```text
docs/
├── data_dictionary.md        # variable names, meanings, units, allowed values
├── decisions_log.md          # major analysis decisions and rationale
├── preprocessing.md          # transformations, assumptions, exclusions
├── qc_rules.md               # QC criteria and interpretation
├── models.md                 # model variants, contrasts, parameter choices
└── onboarding.md             # instructions for new lab members
```

## Decision log template

A decision log (`decisions_log.md`) is a record of why the analysis is structured the way it is. A new entry should be added whenever a choice is made that a collaborator or reviewer could reasonably question. Entries do not need to be long.

```markdown
## YYYY-MM-DD: Decision title

Decision: What was decided?
Reason: Why was this choice made?
Alternatives considered: What else was tried or discussed?
Files affected: Which scripts, data files, reports, or models changed?
Status: Accepted / revised / deprecated
```

## Commenting scripts

Scripts are better documented when they are commented. A comment that restates the syntax adds no information a reader cannot get from the code itself. A useful comment states the reason for the choice: the task assumption, the edge case being handled, or the decision that made this line non-obvious.

**Good comment:**

```python
# Observation trials do not require a response, so they are excluded from
# missed-response counts.
play_trials = df[df["trType"] == 2]
```

**Bad comment:**

```python
# Keep rows where trType is 2.
play_trials = df[df["trType"] == 2]
```

# Rule 10: Make reproducibility a lab default

## Lab-level repository structure

```text
lab-organization/
├── project-template/
├── behavioral-pipeline/
├── neuroimaging-pipeline/
├── analysis-examples/
├── qc-guidelines/
├── onboarding/
└── shared-scripts/
```

## Core onboarding competencies

Every new lab member should complete the following before beginning independent work. These cover the minimum skills on which every subsequent rule depends.

| Competency | What to practice | Relevant rule |
|---|---|---|
| Git and version control | Initialize a repository, make commits with informative messages, create a branch, push to a remote | Rule 2 |
| README and data dictionary in Markdown | Write a project README, populate a data dictionary with variable names, units, and allowed values | Rule 3, Rule 8 |
| Computational environment | Create and activate a virtual environment, record dependencies, recreate from a lock file | Rule 5 |
| AI prompting | Write a bounded AI request that states the task, files/context provided, constraints, protected data, expected output, and review checks. Practice using AI only with code, documentation, schemas, or synthetic/de-identified examples, not raw sensitive data. | Rule 7 |

These competencies should be documented in `docs/onboarding.md` and verified by a lab member before the new analyst begins working on shared data or code.

## Example onboarding package

```text
onboarding/
├── server_access.md
├── project_structure.md
├── how_to_run_pipeline.md
├── how_to_review_qc.md
├── common_errors.md
├── coding_standards.md
└── handoff_checklist.md
```

## Lab reproducibility defaults

Every lab project should have:

- [ ] A standard project template.
- [ ] A root README.
- [ ] A documented environment.
- [ ] A version-controlled repository.
- [ ] A clear data location.
- [ ] A script or workflow entry point.
- [ ] A QC/reporting convention.
- [ ] An onboarding document.
- [ ] A handoff checklist.

## Handoff checklist

Before leaving a project, the analyst should confirm:

- [ ] Repository is pushed to the shared lab organization.
- [ ] README explains how to run the project.
- [ ] Environment file or container version is recorded.
- [ ] Data locations are documented.
- [ ] Pipeline entry point is documented.
- [ ] Outputs and reports are described.
- [ ] QC/exclusion decisions are recorded.
- [ ] Known issues are listed.
- [ ] A new person has tested the instructions.

# Ten simple rules for achieving computational reproducibility in cognitive neuroscience

## Supporting Information [S1 Text]

### About this document

This companion document provides implementation guidance, templates, and working examples for each of the ten rules described in the main article. The content is organized to follow the rules in sequence; each section can also be used as a standalone reference during active project work. Code examples use Python and Bash unless a rule is language-specific, in which case R and MATLAB alternatives are noted. Neuroimaging examples use fMRIPrep as the reference preprocessing pipeline; the underlying principles apply to other pipelines provided the same provenance and environment records are kept. Labs working in different computational environments should treat the examples as starting points and adapt naming conventions, folder structures, and tooling to their own infrastructure.

## Rules

1. [Structure the project before analysis begins](rule-01-project-structure.md)
2. [Implement version control immediately](rule-02-version-control.md)
3. [Document as you build](rule-03-documentation.md)
4. [Convert exploratory work into reusable code](rule-04-reusable-code.md)
5. [Freeze the computational environment](rule-05-environment.md)
6. [Automate repeated steps into scripted workflows](rule-06-automation.md)
7. [Use AI within explicit task boundaries](rule-07-ai-boundaries.md)
8. [Standardize data names, formats, and metadata](rule-08-names-metadata.md)
9. [Account for the data behind each analysis](rule-09-analysis-data.md)
10. [Make reproducibility a lab default](rule-10-lab-defaults.md)

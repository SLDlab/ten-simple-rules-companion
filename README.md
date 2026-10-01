# Ten Simple Rules Companion

Supporting information for:

**Ten simple rules for achieving computational reproducibility in cognitive neuroscience**

[![Documentation](https://img.shields.io/badge/docs-Read%20the%20Docs-blue)](https://ten-simple-rules-companion.readthedocs.io/en/latest/)

This repository hosts the companion documentation for the manuscript, including practical implementation guidance, templates, examples, and reproducibility checklists for each of the ten rules.

## Read the companion

**[Open the documentation](https://ten-simple-rules-companion.readthedocs.io/en/latest/)**

## Contents

1. Structure the project before analysis begins
2. Implement version control immediately
3. Document as you build
4. Convert exploratory work into reusable code
5. Freeze the computational environment
6. Automate repeated steps into scripted workflows
7. Use AI within explicit task boundaries
8. Standardize data names, formats, and metadata
9. Account for the data behind each analysis
10. Make reproducibility a lab default

## Repository

The documentation source is in [`docs/`](docs/) and is built with MkDocs and Material for MkDocs.

Key files:

- [`mkdocs.yml`](mkdocs.yml) — site configuration
- [`.readthedocs.yaml`](.readthedocs.yaml) — Read the Docs build configuration
- [`requirements.txt`](requirements.txt) — documentation dependencies

## Local preview

```bash
pip install -r requirements.txt
mkdocs serve

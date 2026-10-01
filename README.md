# Ten Simple Rules companion documentation

This repository contains the Read the Docs version of the supporting-information companion document for **Ten simple rules for achieving computational reproducibility in cognitive neuroscience**.

The documentation is built with MkDocs and the Material theme and is configured for Read the Docs through `.readthedocs.yaml`.

## Local preview

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
mkdocs serve
```

Then open the local address printed by MkDocs.

## Read the Docs

1. Push this repository to GitHub or another Git provider supported by Read the Docs.
2. Import the repository into Read the Docs.
3. Read the Docs will use `.readthedocs.yaml` and `mkdocs.yml` to build the site.

The content in `docs/` follows the organization of the companion document: an introductory page and one page for each of the ten rules.

# Rule 4: Convert exploratory work into reusable code

## Suggested project code layout

### Scripts

```text
scripts/
├── 00_extract.py
├── 01_preprocess_individual.py
├── 02_merge_group_level.py
├── 03_qc_report.py
├── 04_run_models.py
└── 05_generate_report.py
```

### Source files

```text
src/
├── io.py
├── preprocessing.py
├── qc.py
├── plotting.py
└── models.py
```

### Notebooks

```text
notebooks/
├── exploration.ipynb
└── report.ipynb
```

## Example: repository before and after refactoring

A common mistake in exploratory work is accumulating notebook versions without a clear record of which one produced the reported results. The example below shows the transition from an exploration folder with multiple competing files to a clean scripts layout with a single report notebook.

### Before

```text
notebooks/
├── analysis_final.ipynb
├── analysis_final_v2.ipynb
├── analysis_final_FIXED.ipynb
└── plots_for_paper.ipynb
```

### After

```text
scripts/
├── preprocess.py
├── run_model.py
└── make_figures.py

src/
├── io.py
├── preprocessing.py
├── qc.py
├── plotting.py
└── models.py

notebooks/
└── report.ipynb
```

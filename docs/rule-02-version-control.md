# Rule 2: Implement version control immediately

## Minimal Git setup

```bash
git init
git status
git add README.md .gitignore scripts/ docs/
git commit -m "Initialize reproducible project structure"
```

## Recommended `.gitignore`

```gitignore
# large or generated files
data/raw/
data/intermediate/
data/processed/
derivatives/
work/
logs/
*.nii.gz
*.sif

# local environments
.venv/
env/
__pycache__/

# system files
.DS_Store
```

## Simple commit habit

Use commit messages that explain the change:

**Good:** `Fix taskOL trial labels to separate observe and play events`

**Weak:** `update script`

```bash
git add scripts/build_events.py docs/decisions.md
git commit -m "Add event-building script and document trial-label decisions"
```

## Tag a manuscript or report version

A Git tag gives a readable name to a specific commit, such as the version of the repository used for a manuscript submission, report, or replication package. It does not prevent future changes, but it makes the submitted version easy to find again.

```bash
git tag manuscript-v1
git push origin manuscript-v1
```

## When to use Git alone / When to add large-file version control such as DVC

The decision to add DVC depends on whether the project handles large files that need to be tied to specific code states. For most behavioral projects, Git alone is sufficient. DVC becomes necessary when raw datasets or preprocessing outputs are large enough that storing them in Git would make the repository unwieldy, or when the exact data state that produced a result needs to be recoverable independently of the code.

Use Git alone when the project mainly contains:

- scripts
- README files
- documentation
- configuration files
- small metadata tables
- model specification files
- data dictionaries

Add larger version control tools such as DVC when the project includes:

- large raw datasets
- large derived outputs
- multi-stage preprocessing outputs
- generated QC files
- pipeline outputs that must be linked to exact inputs

DVC documentation: <https://doc.dvc.org/>

## Minimal DVC setup

```bash
dvc init
git add .dvc .dvcignore
git commit -m "Initialize DVC"
```

Track a data directory:

```bash
dvc add data/processed
git add data/processed.dvc .gitignore
git commit -m "Track processed data with DVC"
```

Run a DVC pipeline:

```bash
dvc repro
```

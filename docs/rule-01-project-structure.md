# Rule 1: Structure the project before analysis begins

## Minimal folder layout

```text
project/
├── config/                 # schema, mappings, model settings
├── data/
│   ├── raw/                # immutable inputs
│   ├── intermediate/       # temporary derived files
│   └── processed/          # analysis-ready files
├── docs/                   # decisions, dictionaries, instructions
├── environments/           # environment specifications
├── figures/                # generated figures
├── notebooks/              # exploration
├── reports/                # Quality Control (QC) and analysis reports
├── scripts/                # reusable code
└── README.md
```

This minimal layout above applies to any project. The two examples further below show how it adapts to the two most common data types in the lab. They are not mutually exclusive; a project combining behavioral and imaging data can nest both conventions under the same root.

## Cookiecutter

Cookiecutter is a command-line tool that creates a new project from a reusable template. In this context, the template is stored in a folder or GitHub repository containing three main components: a `cookiecutter.json` file that defines project-specific variables, a templated project directory that defines the files and folders to create, and usually a README explaining how to use the template.

### Example Cookiecutter template

```text
lab-cookiecutter-template/
├── cookiecutter.json              # template variables
└── {{cookiecutter.project_slug}}/
    ├── config/                    # schema, mappings, model settings
    ├── data/
    │   ├── raw/                   # immutable inputs
    │   ├── intermediate/          # temporary derived files
    │   └── processed/             # analysis-ready files
    ├── docs/                      # decisions, dictionaries, instructions
    ├── environments/              # environment specifications
    ├── figures/                   # generated figures
    ├── notebooks/                 # exploration
    ├── reports/                   # QC and analysis reports
    ├── scripts/                   # reusable code
    └── README.md                  # project overview and run instructions
```

This folder shows the reusable project layout that Cookiecutter copies each time a new lab project is created.

The `cookiecutter.json` file defines the variables that Cookiecutter requests when a new project is created:

### Example `cookiecutter.json`

```json
{
  "project_name": "Example neuroscience project",
  "project_slug": "{{ cookiecutter.project_name.lower().replace(' ', '_').replace('-', '_') }}",
  "author_name": "Lab member name",
  "task_name": "task-name",
  "python_version": "3.12"
}
```

The templated directory defines the structure of the generated project. Its name contains the placeholder `{{ cookiecutter.project_slug }}`, which Cookiecutter replaces with the value derived from `project_name`. Other placeholders may similarly be used within file names or file contents.

To create a new project from a template hosted on GitHub, run:

```bash
cookiecutter https://github.com/<lab-org>/<lab-cookiecutter-template>
```

The command points to the GitHub repository containing the complete template. Cookiecutter retrieves the repository, reads `cookiecutter.json`, asks the user for the defined values, and renders the templated directory into a new project directory.

To create the layout from a local template, run:

```bash
cookiecutter /path/to/lab-cookiecutter-template
```

Cookiecutter documentation: <https://cookiecutter.readthedocs.io/en/stable/>

## External widely used templates

The following templates provide ready-made starting points that can be adapted to the lab's conventions. They differ mainly in how they handle the raw/processed split and whether they include R or Python tooling by default.

- Cookiecutter Data Science: standardized data-science project structure.
- govcookiecutter: UK public-sector analytical project template with raw, interim, and processed data folders.
- Alan Turing Institute reproducible-project template: template repository for reproducible research projects.
- Rgovcookiecutter: R-focused version of the UK government analytical project template.

## Example layout from a human-subjects behavioral dataset

```text
behavioral-project/
├── data/
│   └── task_name/
│       ├── task1/
│       │   ├── raw/
│       │   └── preprocessed/
│       │       ├── group_level/
│       │       └── individual_level/
│       ├── task2/
│       ├── task3/
│       └── task4/
├── scripts/
└── README.md
```

## Example layout from a human-subjects imaging dataset

```text
project_name/
├── raw_data/        # scanner exports
├── bids_runs/       # BIDS inputs
├── derivatives/     # fMRIPrep, MRIQC, AROMA outputs
├── work/            # scratch execution state
├── logs/            # run records
├── scripts/         # workflow scripts
├── envs/            # environments
└── *.sif            # pinned containers
```

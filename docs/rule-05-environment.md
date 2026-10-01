# Rule 5: Freeze the computational environment

## Python: lightweight option

The commands below should be used when the project mainly depends on Python packages installed with pip.

Initialize a virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

This creates and activates a local virtual environment, then installs the package versions listed in `requirements.txt`.

Freeze dependencies:

```bash
pip freeze > requirements.txt
```

This records the currently installed Python packages and versions. Commit `requirements.txt` to the repository so another analyst can recreate the environment later.

Recreate the virtual environment:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Use this on a new machine or after deleting the local environment.

## Python: project-file option

Use this option when the project needs a more explicit Python project setup than a basic virtual environment.

`uv` is a Python package and project manager that can create environments, install packages, and write a lock file. Compared with a plain virtual environment, it records project dependencies in `pyproject.toml` and the exact resolved package versions in `uv.lock`, making the environment easier to recreate on another machine.

The commands below should be used when the project is managed with `uv` and should keep a project-level dependency file and lock file.

Initialize a Python project:

```bash
uv init
uv add pandas numpy matplotlib
uv lock
```

This creates a Python project, records dependencies in `pyproject.toml`, and writes the resolved package versions to `uv.lock`.

## R: `renv` option

Use this when the project depends on R packages.

Initialize a virtual environment:

```r
renv::init()       # starts project-level dependency tracking.
renv::snapshot()   # records the current package versions in renv.lock
renv::restore()    # recreates those package versions later.
```

## MATLAB: project option

Use the Graphical User Interface to initialize a MATLAB Project (`.prj`) that will record paths, dependencies, startup tasks, and files needed for the analysis.

## Container option

Use containers when the workflow depends on system libraries, neuroimaging tools, or shared HPC/server environments.

Run a container:

```bash
apptainer exec fmriprep_23.2.1.sif fmriprep --version
```

This checks which version of fMRIPrep is inside the container. A container record should include the image name, version or tag, path, and checksum or digest when available.

### Example container record

```text
containers/
├── fmriprep_23.2.1.sif
├── heudiconv_1.3.3.sif
├── mriqc_23.0.1.sif
└── fmripost_aroma_main.sif
```

# Cookiecutter PyPackage

Cookiecutter template for a Python package

Documentation: <https://bdpedigo.github.io/cookiecutter-pypackage>

## Features

This tool will create Python project with the following features:

- [Poetry](https://python-poetry.org/): Manage dependency, build and release
- [Mkdocs](https://www.mkdocs.org): Writing your docs in markdown style
- Testing with [Pytest](https://pytest.org) (unittest is still supported out of the box)
- [Tox](https://tox.readthedocs.io): Test your code against environment matrix, lint and artifact check
- [Ruff](https://docs.astral.sh/ruff/) for formatting, linting, and import sorting
  - Same functionality as [Black](https://github.com/psf/black), [Isort](https://github.com/PyCQA/isort) and [Flake8](https://flake8.pycqa.org) bundled together
- Check static type with [Mypy](http://mypy-lang.org/) (optional)
- [Pre-commit hooks](https://pre-commit.com/): Formatting/linting anytime when commit your code
- [Mkdocstrings](https://mkdocstrings.github.io/): Auto API doc generation
- Host your documentation from [GitHub Pages](https://pages.github.com) with zero-config
- Continuous Integration/Deployment by [GitHub actions](https://github.com/features/actions), includes:
  - publish dev build to TestPyPI and dev docs automatically when tests pass for each commit to `main`
  - bump version, publish release to PyPI, and publish versioned documentation using a manual GitHub action
  - daily test runs to catch dependency update and CI failure

## Quickstart

To start, you will need [GitHub], [PyPI], and [TestPyPI] accounts. If
you don't have one, please follow the links to apply one before you get started on this
tutorial.

If you are new to Git and GitHub, you should probably spend a few minutes on
some tutorials at the top of the page at [GitHub Help].

### Cookiecutter installation

[Install Cookiecutter](https://github.com/cookiecutter/cookiecutter?tab=readme-ov-file#installation) if you haven't installed it yet (this requires Cookiecutter 1.4.0 or higher).
Currently, since Cookiecutter is itself a python package with its own dependencies,
it is recommended to use [`pipx`](https://github.com/pypa/pipx) to do so:

```bash
pipx install cookiecutter
```

This should enable you to run `cookiecutter` from the command line. To generate a Python
package project using this template, run the following command and follow the prompts:

```bash
cookiecutter https://github.com/bdpedigo/cookiecutter-pypackage.git
```

### Generate your package

Now it's time to generate your Python package.

Run the following command and feed with answers, If you don’t know what to enter, stick with the defaults:

```bash
cookiecutter https://github.com/bdpedigo/cookiecutter-pypackage.git
```

Finally, a new folder will be created under current folder, the name is the answer you
provided to `project_slug`.

Go to this generated folder, the project layout should look like:

```console
.
├── .bumpversion.cfg
├── .editorconfig
├── .github
│   ├── ISSUE_TEMPLATE.md
│   └── workflows
│       ├── dev.yml
│       ├── preview.yml
│       └── release.yml
├── .gitignore
├── .pre-commit-config.yaml
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── README.md
├── docs
│   ├── api.md
│   ├── changelog.md
│   ├── contributing.md
│   ├── index.md
│   ├── installation.md
│   └── usage.md
├── makefile
├── mkdocs.yml
├── my_package
│   ├── __init__.py
│   ├── cli.py
│   └── my_package.py
├── pyproject.toml
├── setup.cfg
└── tests
    ├── __init__.py
    └── test_my_package.py

```

Here the project_slug is `my-package`, when you generate yours, it could be other name.

Also be noticed that there's `pyproject.toml` in this folder. This is the main configuration file of our project.

### Create a GitHub repo

Create a [new GitHub repo](https://github.com/new). Do not initialize with a README or
any other files.

Follow the instructions there for uploading your existing repo from the command line. It
should look something like this (where { owner name } is your GitHub username and { repo name } is the name of your repo):

```
git init
git add .
git commit -m "initial commit"
git branch -M main
git remote add origin https://github.com/{ owner name }/{ repo name }.git
git push -u origin main
```

### Install Poetry

Next, install [Poetry](https://python-poetry.org/) if you haven't already. I recommend
installing according to their most recent [instructions](https://python-poetry.org/docs/#installation).
As of this writing, the recommended way to install Poetry is with [pipx](

```bash
pipx install poetry
```

In addition, Poetry provides a [custom installer](https://python-poetry.org/docs/#installation) that will install
poetry isolated from the rest of your system by vendorizing its dependencies.
This is the recommended way of installing poetry.

### Install developer requirements

You should still be in the folder named `project_slug`, which contains the
`pyproject.toml` file.

It is a good idea to make a new virtual environment, although Poetry will also do this
automatically for you in the next step. If you would like to do this manually, you can
use the following command:

```bash
poetry env use <path to Python interpreter>
```

For instance, to use the Python 3.11 interpreter linked to the alias `python3.11`,
you would run:

```bash
poetry env use python3.11
```

By default, this will create a virtual environment in the `.venv` folder in your project
directory. To activate this virtual environment, run:

```bash
source .venv/bin/activate
```

or

```bash
poetry shell
```

With the environment active, install the new project's local development requirements
with `poetry install`:

```bash
poetry install --with dev
```

Poetry will create its own virtualenv isolated from your system and install the dependencies in it.
We installed extra dependency needed by developers with the `--with dev` option, such as
documentation build tools, linting, formatting and test tools etc.

### Run tests

We also launch a test here by running `poetry run tox`. This will run `tox` within
created virtual environment, give you a test report and lint report. You should see no
errors except some lint warnings.

```bash
poetry run tox
```

If you found errors like the following during tox run:

```
ERROR: InterpreterNotFound: python3.9
```

don't be panic, this is just because python3.x is not found on your machine. If you
decide to support that version of Python in your package, please install it on your
machine. Otherwise, remove it from tox.ini and pyproject.toml (search python3.x then
remove it).

### Change GitHub settings

On GitHub, go to your new repo and click on the "Settings" tab. Then click on "Actions" in the left sidebar.
Under "Workflow permissions", check the box for "Read and write permissions".

### Initialize documentation

```
mike deploy --push --update-aliases dev
```

### Set up publishing

- Go to PyPI
- Log in
- In your account, go to Publishing
   - You may need to set up 2FA at this point  
- Hit "Add a new pending publisher"
- Under GitHub, fill out the details of your package
   - Use `release.yml` under "Workflow name"
- If setting up TestPyPI, do all of the above again on TestPyPI, but use `test-release.yml` as the workflow.
- If you make a commit on the repo, TestPyPI should automatically cut a pre-release version.

### Create a release

You can cut a release using the pre-made GitHub action. Go to the repo on GitHub, hit the "Actions" tab, and click "publish release." You should see a button on the top right that says "Run workflow." Uncheck "dry run" and run the workflow for a "patch" bump just to test things out.  

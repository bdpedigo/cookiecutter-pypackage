# Cookiecutter PyPackage

Cookiecutter template for a Python package, built with popular develop tools and conform to best practice.

- Documentation: <https://bdpedigo.github.io/cookiecutter-pypackage>

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

Install the latest Cookiecutter if you haven't installed it yet (this requires Cookiecutter 1.4.0 or higher):

```
pip install -U cookiecutter
```

Generate a Python package project:

```
cookiecutter https://github.com/bdpedigo/cookiecutter-pypackage.git
```

Then follow **[Tutorial](docs/tutorial.md)** to finish other configurations.

## Credits

This repo is forked from [waynerv/cookiecutter-pypackage](https://github.com/waynerv/cookiecutter-pypackage), which forked from [zillionare/python-project-wizard](https://github.com/zillionare/python-project-wizard), which forked from [audreyfeldroy/cookiecutter-pypackage](https://github.com/audreyfeldroy/cookiecutter-pypackage).

sources = {{ cookiecutter.pkg_name }}

.PHONY: test format lint unittest coverage pre-commit clean
test: format lint unittest

format:
	ruff format $(sources) tests

lint:
	ruff check $(sources) tests
	{%- if cookiecutter.use_mypy == 'y' %}
	mypy $(sources) tests
	{%- endif %}

unittest:
	pytest

pre-commit:
	pre-commit run --all-files

clean:
	rm -rf {% if cookiecutter.use_mypy == 'y' -%}.mypy_cache {% endif -%} .pytest_cache
	rm -rf *.egg-info
	rm -rf .tox dist site
	rm -rf coverage.xml .coverage

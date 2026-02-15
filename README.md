# sample-python-semantic-release

A sample python library project with Github actions workflows automating the publication of a new version in PyPI (in test PyPI, to keep PyPI sane).

Expected behavior when merging a PR on the `main` branch:
- run the code-quality workflow
  - lint
  - test
- on success, run the release workflow
  - use the [Python semantic release tool](https://python-semantic-release.readthedocs.io/en/latest/) to compute the next version base on the conventional commit messages
  - update the `CHANGELOG.md` file
  - apply a tag corresponding to the new version
  - if the commits lead to a new version, deploy on test-PyPI (to not pollute the PyPI repo with junk code)

## Code linting

Configured by pre-commit hooks

```sh
# install pre-commit hooks on the repo (once for all)
uv run pre-commit install

# run hooks on staged files
uv run pre-commit run

# run hooks on all files
uv run pre-commit run --all-files

# update the hooks version
uv run pre-commit autoupdate
```

## Automated tests

```sh
# without coverage
uv run pytest

# with coverage
uv run pytest -v --cov=sample_python_semantic_release --cov-branch --cov-report term-missing --cov-fail-under 95
```

## How the python project was initialized

```sh
uv init --lib --no-workspace --python 3.14.3 --name sample-python-semantic-release
```

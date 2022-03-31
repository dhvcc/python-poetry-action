# Python poetry setup action

Action that allows you to quickly set-up python and poetry with caching included.

As a nice bonus it also caches pre-commit's downloads

## Example

Example workflow with matrix strategy and using pre-commit to lint files

```yaml
name: Lint

on:
  pull_request:
  push:
    branches: [ master, develop ]

jobs:
  lint:
    strategy:
      matrix:
        os: [ubuntu-latest]
        python-version: [3.8]

    runs-on: ${{ matrix.os }}
    steps:
      - uses: dhvcc/python-poetry-setup@master
        with:
          python-version: ${{ matrix.python-version }}
          cache-key: ${{ matrix.os }}-${{ matrix.python-version }}-pip-${{ hashFiles('**/poetry.lock') }}

      - name: Lint
        run: |
          poetry run pre-commit run --all-files

```

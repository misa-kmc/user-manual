## MISA-AKMC Users Manual

## Build and serve document
### Install dependencies
First, you should install [poetry](https://python-poetry.org) python package manager on your system.
Then run for to install mkdocs and mkdocs-material theme:
```bash
poetry install # install mkdocs(https://www.mkdocs.org) and mkdocs-material
```

### Serve document
run `poetry run mkdocs serve` to preview document site, then open your browser and visit `http://localhost:8000`.

### Build document
run `poetry run mkdocs build` to build a static site.

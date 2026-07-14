# cookiecutter-azure-repos

A collection of [Cookiecutter](https://cookiecutter.readthedocs.io/) templates for scaffolding
Azure-hosted project repos with a consistent structure and a ready-to-run Azure Pipelines YAML
(compile/build, SCA, SAST, test).

Each template lives in its own git repo, included here as a submodule and grouped by
**language + function** (e.g. Python Function App, Python Container App), so each generated
project has a structure and pipeline shaped for what it actually does rather than one
template trying to cover every case.

## Templates

| Template | Path | Description |
|---|---|---|
| Python Function App | [`cookiecutter-python-functionapp`](cookiecutter-python-functionapp) | Azure Functions (Python) project. Pipeline: Build, SCA (pip-audit), SAST (bandit), Test (pytest). |
| Python Container App | [`cookiecutter-python-containerapp`](cookiecutter-python-containerapp) | FastAPI service with Dockerfile for Azure Container Apps. Pipeline: SCA (pip-audit), SAST (bandit), Test (pytest), Build & Push to ACR. |

More templates (e.g. Python Data Pipeline, Python Workbook) will be added the same way.

## Getting started

Clone with submodules:

```bash
git clone --recurse-submodules <this-repo-url>
```

If you already cloned without `--recurse-submodules`:

```bash
git submodule update --init --recursive
```

## Generating a project from a template

```bash
pip install cookiecutter
cookiecutter cookiecutter-python-functionapp
# or
cookiecutter cookiecutter-python-containerapp
```

Answer the prompts, then push the generated project to its own Azure DevOps repo.

## Adding a new template

1. Create a new repo, e.g. `cookiecutter-python-datapipeline`, following the same layout as the
   existing templates (`cookiecutter.json`, `{{cookiecutter.project_slug}}/`, optional `hooks/`).
2. Add it as a submodule here:
   ```bash
   git submodule add <repo-url> cookiecutter-python-datapipeline
   ```
3. Add a row to the table above.

## Notes

- Submodule URLs currently point to local paths until these repos are pushed to Azure DevOps —
  update `.gitmodules` with the real remote URLs at that point.
- Shared Azure Pipelines step templates (for reuse across project types) may be extracted into
  a separate templates repo once there's enough duplication to justify it.

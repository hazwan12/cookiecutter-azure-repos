# cookiecutter-azure-repos

A collection of [Cookiecutter](https://cookiecutter.readthedocs.io/) templates for scaffolding
Azure-hosted project repos with a consistent structure and a ready-to-run Azure Pipelines YAML
(security scan, SCA, SAST, test, build-once-deploy-many).

Each template lives in its own git repo, included here as a submodule and grouped by
**language + function** (e.g. Python Function App, Python Container App), so each generated
project has a structure and pipeline shaped for what it actually does rather than one
template trying to cover every case.

## Templates

| Template | Path | Description |
|---|---|---|
| Python Function App | [`cookiecutter-python-functionapp`](https://github.com/hazwan12/cookiecutter-python-functionapp) | Azure Functions (Python) project. Pipeline: Defender for DevOps, SCA (CodeQL Dependency Scanning or pip-audit), SAST (CodeQL or Bandit), Test (pytest), Build, illustrative Deploy to UAT/Production. |
| Python Container App | [`cookiecutter-python-containerapp`](https://github.com/hazwan12/cookiecutter-python-containerapp) | FastAPI service with Dockerfile for Azure Container Apps. Pipeline: Defender for DevOps, SCA (CodeQL Dependency Scanning or pip-audit), SAST (CodeQL or Bandit), Test (pytest), Build & Push to ACR, illustrative Deploy to UAT/Production. |

More templates (e.g. Python Data Pipeline, Python Workbook) will be added the same way.

## Getting started

Clone with submodules:

```bash
git clone --recurse-submodules https://github.com/hazwan12/cookiecutter-azure-repos.git
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

Answer the prompts, then push the generated project to its own repo (Azure DevOps or GitHub).

## Adding a new template

1. Create a new repo, e.g. `cookiecutter-python-datapipeline`, following the same layout as the
   existing templates (`cookiecutter.json`, `{{cookiecutter.project_slug}}/`, optional `hooks/`).
2. Add it as a submodule here:
   ```bash
   git submodule add <repo-url> cookiecutter-python-datapipeline
   ```
3. Add a row to the table above.

## Notes

- The `DeployUAT` / `DeployProduction` stages in each pipeline are illustrative examples of a
  build-once-deploy-many flow, not production-ready as-is — real release pipelines should be
  configured in Azure DevOps under Pipelines > Releases (or an equivalent environment-gated
  YAML pipeline maintained separately).
- CodeQL-based SAST/SCA options require GitHub Advanced Security for Azure DevOps to be enabled
  on the target repo; if it isn't licensed, regenerate with `sast_tool=bandit` / `sca_tool=pip-audit`.
- Shared Azure Pipelines step templates (for reuse across project types) may be extracted into
  a separate templates repo once there's enough duplication to justify it.

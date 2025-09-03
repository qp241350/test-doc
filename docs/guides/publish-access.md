# Publish and Access TechDocs

This guide explains how to publish your TechDocs and access them in Backstage using the centralized repository and PR workflow.

## 1) Ensure required files exist

In this central repository (https://github.qmul.ac.uk/newworld/backstage-docs), your component folder should contain, at minimum:

- `catalog-info.yaml` with `backstage.io/techdocs-ref: dir:.`
- `mkdocs.yml` with `plugins: [techdocs-core]` and `docs_dir: docs`
- `docs/` directory with `index.md` and other pages

Example `catalog-info.yaml` snippet:

```yaml
apiVersion: backstage.io/v1alpha1
kind: Component
metadata:
  name: your-component-name
  annotations:
    backstage.io/techdocs-ref: dir:.
spec:
  type: service
  owner: your-team
  lifecycle: production
```

Example `mkdocs.yml` snippet:

```yaml
site_name: Your Component Docs
plugins:
  - techdocs-core
docs_dir: docs
```

## 2) Create a branch and open a PR

- Create a feature branch in this repo (e.g., `feature/your-component-docs`).
- Commit your changes to that branch and push.
- Open a Pull Request to merge into `main`.
- Backstage is pre-configured to automatically discover catalog entities from the `main` branch of this repository only.

## 3) Open Backstage and sign in

- Navigate to: https://unified.a.comp-teach.qmul.ac.uk/
- Sign in using your Queen Mary (QMUL) account.

## 4) Find your docs

- Look for your component by `metadata.name` in backstage.
- Open the component page and click the "Docs" tab.
- Backstage will generate and serve your TechDocs from `main` after your PR is merged.

## 5) Troubleshooting

- Missing Docs tab: verify `backstage.io/techdocs-ref` annotation.
- Broken "Edit this page" links: set `repo_url` and `edit_uri` in `mkdocs.yml`.
- Content not updating: ensure your PR was merged to `main` (Backstage only reads from `main`).

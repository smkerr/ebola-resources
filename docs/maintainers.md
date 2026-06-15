# Maintainers Guide

## How resources get added

### Automated flow (issue form)

1. A community member opens a GitHub Issue using the "Suggest a Resource" form
2. A GitHub Action creates a `.md` file in `docs/_incoming/` and opens a Pull Request
3. The maintainer reviews the PR, moves the file to the correct section directory, adds it to `myst.yml`, and merges
4. A deploy workflow builds and publishes the updated site

### Direct PRs

Technical contributors may open PRs with new `.md` files or edits to existing ones. The maintainer adds any new files to `myst.yml` during review.

## Site structure

```
myst.yml                    ← site config + TOC (you control this)
docs/
  intro.md                  ← landing page
  dashboards/               ← one .md file per resource
  epi-parameters/
  outbreak-size-estimates/
  risk-of-spread/
  mobility-data/
  humanitarian-data/
  therapeutics-vaccines/
  _incoming/                ← staging area for automation-created files
  contributing.md
  maintainers.md
```

## Managing structure

The site navigation is defined entirely by the `toc:` section in `myst.yml`. You have full control over sections, sub-sections, and ordering.

### Adding a resource to the site

Add one line to `myst.yml` under the appropriate section:

```yaml
- title: Dashboards
  children:
    - file: docs/dashboards/inrb-umie-dashboard
    - file: docs/dashboards/new-resource        # ← add here
```

### Creating a new section

```yaml
- title: New Section Name
  children:
    - file: docs/new-section/first-resource
```

Then update the section dropdown in `.github/ISSUE_TEMPLATE/new-resource.yml`.

### Creating sub-sections

```yaml
- title: Epidemiology
  children:
    - title: Parameters
      children:
        - file: docs/epi-parameters/grepi-perg
    - title: Estimates
      children:
        - file: docs/outbreak-size-estimates/mccabe-imperial
```

### Reordering or moving resources

Rearrange the lines in `myst.yml`. Move `.md` files between directories if you want the file paths to match.

## Local development

```bash
pip install jupyter-book
jupyter-book start
```

The site builds at `http://localhost:3000/`.

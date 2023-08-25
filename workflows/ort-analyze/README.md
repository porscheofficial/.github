# OSS Review Toolkit

This reusable GitHub Action workflow uses the [OSS Review Toolkit]([https://github.com/todogroup/repolinter](https://github.com/oss-review-toolkit/ort))
to create all necessary metadata information needed to ensure FOSS compliance of our FOSS projects.

## How to use

To implement this worklow in your repository, create a file named `oso-analyzer.yml` under `.github/workflows` and add the following content:

```yaml
name: OSO ORT Analyzer

on:
  workflow_dispatch:

jobs:
  # =============================================================================
  # JOB: ANALYZER
  # =============================================================================
  analyzer:
    runs-on: ubuntu-latest
    name: OSO ORT
    steps:
      - uses: actions/checkout@v3
      - name: Run OSO ORT Analyzer
        id: analyzer
        uses: porscheofficial/.github/workflows/ort-analyze@main
        with:
          ort-aws-access-key-id: ${{ secrets.ANALYZER_AWS_ACCESS_KEY_ID }}
          ort-aws-secret-access-key: ${{ secrets.ANALYZER_AWS_ACCESS_KEY }}
          container-repository: ${{ secrets.ANALYZER_DOCKER_IMAGE }}
          container-registry: ${{ secrets.ANALYZER_DOCKER_REGISTRY }}
```

The secrets `ANALYZER_AWS_ACCESS_KEY_ID`, `ANALYZER_AWS_ACCESS_KEY`, `ANALYZER_DOCKER_IMAGE`, `ANALYZER_DOCKER_REGISTRY` are defined organization-wide
for public repositories. Should you work on a private repository within @porscheofficial, please add the secrets manually as defined in our coporate wiki.

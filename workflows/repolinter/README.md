# OSO Repolinter

This reusable GitHub Action workflow uses the [TODO Group repolinter](https://github.com/todogroup/repolinter) to check a repository against the standards
we at Porsche endorse for new FOSS projects.

## How to use

To implement this worklow in your repository, create a file named `oso-repolinter.yml` under `.github/workflows` and add the following content:

```yaml
name: OSO Repolinter

on: [push, workflow_dispatch]

jobs:
  # =============================================================================
  # JOB: REPOLINTER
  # =============================================================================
  analyzer:
    runs-on: ubuntu-latest
    name: OSO Repolinter
    steps:
      - uses: actions/checkout@v3
      - name: Run OSO Repolinter
        id: repolinter
        uses: porscheofficial/.github/workflows/repolinter@main
        with:
          is-distributed: false
```

Please set `is-distributed` to `true` should you distribute third-party components, i.e. if you have received a compulsory Open-Source Software Notice
from the Porsche Open Source Office.

## Rulesets

The general ruleset that applies to all FOSS projects maintained by Porsche can be found in the [`general-ruleset.yml`](general-ruleset.yml) file.
The [`distribution-ruleset.yml`](distribution-ruleset.yml) applies to all projects that distribute third-party packages.

## Contributing

Contributions to our repolinter rulesets are highly appreciated. Please open an issue or pull request to propose a change to our project standards.

# trestle-assemble-release
https://github.com/marketplace/actions/merge-assemble-release


This is a Github Action for assembling trestle project and automated releasing with semantic versioning.
This actions is triggered when a pull request is merged into the main branch.

## Requirements
If the project is not a trestle project (https://github.com/IBM/compliance-trestle), this action will fail. Hence, the top level source directory must be a trestle project.
The version of the trestle project is identified by the `version` key in each of the top level OSCAL models, e.g. `catalog.json`. Having different versions on different models will result in version conflict and action will fail.
The version tag has to be semantic versioning, i.e. x.x.x (major.minor.patch), and the version bump is automatically triggered by commit messages, following Angular Commit convention here https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits .

1. Must checkout the trestle git project. (uses: actions/checkout@v2)
2. Must install python. (uses: actions/setup-python@v2)

## Known Issues/ Work in Progress
1. Workflow is hardcoded to assemble json files only. In near future, it should accept an configuration for desired file type and/or figure out file type from the source models.

## Usage
Import this action into your workflow using `uses` key:
```
name: assemble-release
on:
  pull_request:
    branch: main
    # Run only for closed PR
    types: [ closed ]

jobs:
  merge_job:
    # Run only if PR is merged into Main
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest
    steps:
        # Pre-requisite 1
      - name: Checkout git project
        uses: actions/checkout@v2
        # Pre-requisite 2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: 3.8


      - name: trestle-assemble-release
        uses: compliance-trestle/trestle-assemble-release@2.2.0

```

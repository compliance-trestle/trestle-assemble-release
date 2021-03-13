# trestle-assemble-release
https://github.com/marketplace/actions/merge-assemble-release


This is a Github Action for assembling trestle project and automated releasing with semantic versioning.
This actions is triggered when a pull request is merged into the main branch.

## Requirements
If the project is not a trestle project (https://github.com/IBM/compliance-trestle), this action will fail. Hence, the top level source directory must be a trestle project.
The version of the trestle project is identified by the `version` key in each of the top level OSCAL models, e.g. `catalog.json`. Having different versions on different models will result in version conflict and action will fail.
The version tag has to be semantic versioning, i.e. x.x.x (major.minor.patch), and the version bump is automatically triggered by commit messages, following Angular Commit convention here https://github.com/angular/angular/blob/master/CONTRIBUTING.md#commit .

## Usage
Import this action into your workflow using `uses` key:
```
uses: compliance-trestle/trestle-assemble-release
```

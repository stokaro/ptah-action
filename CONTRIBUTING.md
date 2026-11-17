# Contributing

This repository is a published copy. The action's single source is
[`.github/actions/ptah`](https://github.com/stokaro/ptah/tree/master/.github/actions/ptah)
in [`stokaro/ptah`](https://github.com/stokaro/ptah), and a workflow there
mirrors the directory here on every change.

Changes to action files, including `AGENTS.md`, belong in `stokaro/ptah`
under `.github/actions/ptah`. Direct edits to those files in this repository
are overwritten by the next publication. `scripts/check-action-publishable.sh`
runs on the source pull request and checks that the action can be published.

The `.github/` directory and this `CONTRIBUTING.md` are maintained here and
preserved by the publication workflow. Changes to the PR template or smoke
workflow belong in this repository.

## Pull requests

Use the [PR template](.github/pull_request_template.md) and follow
[Pull request descriptions](AGENTS.md#pull-request-descriptions).
Explain the affected workflow, resulting behavior, risks, and observed
verification. Link a required source change when the PR depends on one.

Issues are welcome here.

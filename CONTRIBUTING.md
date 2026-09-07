# Contributing

This repository is a published copy. The action's single source is
[`.github/actions/ptah`](https://github.com/stokaro/ptah/tree/master/.github/actions/ptah)
in [`stokaro/ptah`](https://github.com/stokaro/ptah), and a workflow there
mirrors the directory here on every change.

So a pull request against this repository is overwritten by the next publish,
however good it is. Open it against `stokaro/ptah` instead, editing the files
under `.github/actions/ptah`. `scripts/check-action-publishable.sh` runs on
that pull request and refuses a change that could not be published.

Issues are welcome here.

# Contributing to Phemera enhancements

Thanks for your interest in contributing. This repository holds Phemera Enhancement Proposals (PEPs). This guide explains how to open a pull request here and what we look for in it.

Please follow our [Code of Conduct](CODE_OF_CONDUCT.md) in all project spaces.

## Before you start

To propose a new PEP, open an issue using the "PEP tracking issue" template first and describe the problem. The [README](README.md) summarizes when a PEP is needed and how to submit one, and [PEP-0001](peps/0001-pep-process/README.md) defines the full process. Typo fixes and other small corrections to existing PEPs can go straight to a pull request.

## Making a change

1. Fork the repository and create a branch for your change.
2. Make your change and sign off every commit (see [Developer Certificate of Origin](#developer-certificate-of-origin)).
3. Run `scripts/validate-peps.py` locally, then open a pull request against `main`.
4. A maintainer reviews the pull request and may ask for changes.
5. Once it is approved, a maintainer squash merges it.

Every pull request needs one approval from a maintainer other than its author before it can be merged. If someone pushes to the pull request after the approval, it needs a new approval from someone other than that person. A PEP needs more approvals before its status changes, as [PEP-0001](peps/0001-pep-process/README.md#approval) explains.

## Pull request titles

Pull requests are squash merged, so the pull request title becomes the commit message on `main`. Titles must follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<optional scope>): <description>
```

For example:

- `docs: add PEP-0004 for SSH session recording`
- `docs(pep-0003): describe the role hierarchy`
- `fix: correct the status check in validate-peps.py`

Allowed types are `build`, `chore`, `ci`, `docs`, `feat`, `fix`, `perf`, `refactor`, `revert`, `style` and `test`. For a breaking change, add `!` after the type or scope, for example `feat!: require a tracking issue for every PEP`.

A check on every pull request validates the title. The commit messages inside your branch do not have to follow this format.

## Developer Certificate of Origin

All contributions must be signed off under the [Developer Certificate of Origin](https://developercertificate.org/) (DCO). By signing off, you confirm that you wrote the change or have the right to submit it under the project's license.

To sign off a commit, add `-s` to `git commit`:

```sh
git commit -s -m "docs: describe the role hierarchy"
```

This adds a line like this to the commit message:

```
Signed-off-by: Jane Doe <jane@example.com>
```

The email in this line must match the commit author. A check on every pull request makes sure all commits are signed off.

If you forgot to sign off, you can add the sign-off to all commits on your branch and update the pull request:

```sh
git rebase --signoff main
git push --force-with-lease
```

## License

By contributing, you agree that your contributions are licensed under the [Apache License 2.0](LICENSE), the same license as Phemera.

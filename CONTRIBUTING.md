# Contributing

This guide is for anyone who wants to fix or improve the Avocado extension in this repository.

## Where to start

- Report a bug or propose a change in this repository's GitHub issues.
- Ask questions on [Discord](https://www.peridio.com/join-our-discord).

## Test a change locally

Run these commands from the repository root, where `avocado.yaml` lives. Replace `avocado-ext-<name>` with the extension key in `avocado.yaml`. Replace `qemux86-64` with the `target` of a row in `.github/workflows/test.yml`.

```sh
export AVOCADO_DISTRO_RELEASE=2024 AVOCADO_DISTRO_CHANNEL=next
avocado sdk install --target qemux86-64
avocado ext install avocado-ext-<name> --target qemux86-64
avocado ext build avocado-ext-<name> --target qemux86-64
```

The two variables select the package feed and the SDK image tag. Set them to the `distro-release` and `distro-channel` of the same matrix row.

## Pull request checks

The Test workflow in `.github/workflows/test.yml` runs on every pull request. It calls `extension-test.yml` from `avocado-linux/actions@v1` once per matrix row. Each row installs the avocado CLI and runs `avocado sdk install`, `avocado ext install` and `avocado ext build` for that row's target and feed. The check builds the extension and never packages or publishes it.

## Releases

You cut a release by pushing a tag equal to the `version` in `avocado.yaml`, for example `git push origin 0.1.0`. Use a bare version shaped `X.Y.Z` or `X.Y.Z-*`. A tag with a `v` prefix does not start the Release workflow.

The Release workflow packages the extension and publishes it to the feed of each matrix row in `.github/workflows/release.yml`. It fails the publish if the tag does not equal the `avocado.yaml` version. The workflow can also be run by hand from the Actions tab. A manual run on a branch skips the tag check and publishes whatever version `avocado.yaml` holds.

## Changelog

Record notable changes in `CHANGELOG.md`. The file follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versions follow [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## Security issues

Do not report a security vulnerability in a public issue, pull request or Discord. Report it privately as the [Avocado security policy](https://github.com/avocado-linux/avocado-cli/blob/main/SECURITY.md) describes. Use **Report a vulnerability** on the avocado-cli Security tab, or email info@peridio.com. Name the affected repository in your report.

## License

This repository is licensed under the Apache License 2.0. See the repository's LICENSE file.

Section 5 of the license covers contributions. Unless you explicitly state otherwise, any contribution you intentionally submit for inclusion is under the terms of the Apache License 2.0, without any additional terms or conditions.

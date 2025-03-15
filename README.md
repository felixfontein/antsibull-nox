<!--
Copyright (c) Ansible Project
GNU General Public License v3.0+ (see LICENSES/GPL-3.0-or-later.txt or https://www.gnu.org/licenses/gpl-3.0.txt)
SPDX-License-Identifier: GPL-3.0-or-later
-->

# antsibull-nox -- Antsibull Nox Helper
[![Discuss on Matrix at #antsibull:ansible.com](https://img.shields.io/matrix/antsibull:ansible.com.svg?server_fqdn=ansible-accounts.ems.host&label=Discuss%20on%20Matrix%20at%20%23antsibull:ansible.com&logo=matrix)](https://matrix.to/#/#antsibull:ansible.com)
[![Nox badge](https://github.com/ansible-community/antsibull-nox/workflows/nox/badge.svg?event=push&branch=main)](https://github.com/ansible-community/antsibull-nox/actions?query=workflow%3A%22nox%22+branch%3Amain)
[![Codecov badge](https://img.shields.io/codecov/c/github/ansible-community/antsibull-nox)](https://codecov.io/gh/ansible-community/antsibull-nox)
[![REUSE status](https://api.reuse.software/badge/github.com/ansible-community/antsibull-nox)](https://api.reuse.software/info/github.com/ansible-community/antsibull-nox)

A [nox](https://nox.thea.codes/en/stable/) helper for Ansible collections.

antsibull-nox is covered by the [Ansible Code of Conduct](https://docs.ansible.com/ansible/latest/community/code_of_conduct.html).

## Community

Need help or want to discuss the project? See our [Community guide](https://ansible.readthedocs.io/projects/antsibull-nox/community/) to learn how to join the conversation!

## Installation

It can be installed with pip:

    pip install antsibull-nox

## Development

Install and run `nox` to run all tests. That's it for simple contributions!
`nox` will create virtual environments in `.nox` inside the checked out project
and install the requirements needed to run the tests there.

---

antsibull-nox depends on the sister antsibull-fileutils project.
By default, `nox` will install a development version of this project from Github.
If you're hacking on antsibull-fileutils alongside antsibull-nox,
nox will automatically install this project from `../antsibull-fileutils`
when running tests if those paths exist.
You can change this behavior through the `OTHER_ANTSIBULL_MODE` env var:

- `OTHER_ANTSIBULL_MODE=auto` — the default behavior described above
- `OTHER_ANTSIBULL_MODE=local` — install the project from `../antsibull-fileutils`.
  Fail if that path doesn't exist.
- `OTHER_ANTSIBULL_MODE=git` — install the projects from the Github main branch
- `OTHER_ANTSIBULL_MODE=pypi` — install the latest versions from PyPI

---

To run specific tests:

1. `nox -e test` to only run unit tests;
4. `nox -e lint` to run all linters and formatters at once;
5. `nox -e formatters` to run `isort` and `black`;
3. `nox -e codeqa` to run `flake8`, `pylint`, `reuse lint`, and `antsibull-changelog lint`;
7. `nox -e typing` to run `mypy`.

## Creating a new release:

1. Run `nox -e bump -- <version> <release_summary_message>`. This:
   * Bumps the package version in `src/antsibull_nox/__init__.py`.
   * Creates `changelogs/fragments/<version>.yml` with a `release_summary` section.
   * Runs `antsibull-changelog release` and adds the changed files to git.
   * Commits with message `Release <version>.` and runs `git tag -a -m 'antsibull-nox <version>' <version>`.
   * Runs `hatch build --clean`.
2. Run `git push` to the appropriate remotes.
3. Once CI passes on GitHub, run `nox -e publish`. This:
   * Runs `hatch publish`;
   * Bumps the version to `<version>.post0`;
   * Adds the changed file to git and run `git commit -m 'Post-release version bump.'`;
4. Run `git push --follow-tags` to the appropriate remotes and create a GitHub release.

## License

Unless otherwise noted in the code, it is licensed under the terms of the GNU
General Public License v3 or, at your option, later. See
[LICENSES/GPL-3.0-or-later.txt](https://github.com/ansible-community/antsibull-nox/tree/main/LICENSE)
for a copy of the license.

The repository follows the [REUSE Specification](https://reuse.software/spec/) for declaring copyright and
licensing information. The only exception are changelog fragments in ``changelog/fragments/``.

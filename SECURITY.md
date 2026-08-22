# Security

## Reporting a vulnerability

Please do not open a public GitHub issue for security problems. Report it
directly:

- **E-mail:** info@thectic.nl
- **PGP key:** <https://thectic.nl/.well-known/openpgpkey/hu/mg6owx9w8c3ejg3tu31f4tha5n17d4rj>

The signed, canonical contact details live in
[security.txt](https://thectic.nl/.well-known/security.txt).

> When a site built from this template gets its own domain, point the line above
> at that site's own `security.txt` and update the `Canonical:` field inside it.

You will hear back within a few days.

## What is worth reporting

A site built from this template is static: HTML, CSS, a little JavaScript and
some images on a CDN. There is no database, no login screen and no visitor data
is stored. Reports are most useful when they are about:

- the templates and the build (`src/layouts/`, `src/assets/`)
- the site's own configuration (headers, DNS, CDN, `security.txt`)
- the small amount of JavaScript the site ships in `src/assets/js/`
- the GitHub Actions workflows in `.github/workflows/`

Output from an automated scanner without demonstrable impact on any of the
above is not very useful.

## Dependencies

There is no package manager. Hugo and the CI tooling are pinned to a version
and a SHA-256 checksum, GitHub Actions to a commit SHA. Renovate opens pull
requests for updates; see [README.md](./README.md#dependency-updates).

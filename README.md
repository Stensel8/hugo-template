# Hugo Site Template

A minimal Hugo starter with dark/light mode, a card component, and a GitHub link in the footer.

| Light | Dark |
|-------|------|
| ![Light mode preview](preview-light.avif) | ![Dark mode preview](preview-dark.avif) |

## Repo structure

```
hugo-template/
├── src/                  # Hugo project root (hugo.toml, assets, layouts)
│   ├── assets/
│   ├── layouts/
│   └── hugo.toml
├── preview-light.avif
├── preview-dark.avif
├── LICENSE
└── README.md
```

Hugo commands are run from inside `src/`. Everything at the repo root is project metadata.

## Usage

```bash
git clone https://github.com/THectic-NL/hugo-template.git
cd hugo-template/src
hugo server
```

Install Hugo **extended**, in the version the CI uses (see
[`.github/actions/setup-hugo/action.yml`](.github/actions/setup-hugo/action.yml)).

## Starting a new site from this template

Everything below already works on a fresh copy; the deploy is the only part
that needs anything from you.

1. Set the repository secrets for Bunny. Until `BUNNY_STORAGE_ZONE` exists the
   deploy workflow stops with a notice instead of failing, so a new site stays
   green while you get round to it.

   | Secret | What it is |
   | --- | --- |
   | `BUNNY_STORAGE_ZONE` | storage zone name |
   | `BUNNY_ACCESS_KEY` | storage zone password |
   | `BUNNY_STORAGE_ENDPOINT` | e.g. `https://storage.bunnycdn.com` |
   | `BUNNY_API_KEY` | account API key, only for purging |
   | `BUNNY_PULL_ZONE_ID` | pull zone to purge, only for purging |

2. Change `baseURL` and `title` in `src/hugo.toml`, and trim `disableKinds` to
   whatever the site actually needs. It ships with almost everything off.

3. Delete `preview-light.avif`, `preview-dark.avif` and this section.

## CI/CD

Four workflows. Every action is pinned to a commit SHA, and every tool that gets
downloaded is pinned to a version and a checksum.

| Workflow | What it does |
| --- | --- |
| `quality.yml` | Two jobs: **site** (Hugo build with `--panicOnWarning`, HTMLHint, offline link check) and **repo** (markdownlint, actionlint, zizmor) |
| `security.yml` | Semgrep on every push and pull request; OpenSSF Scorecard weekly and on `main` |
| `config-validation.yml` | Validates `renovate.json` and `dependabot.yml` — the configs nothing else exercises |
| `deploy-bunny.yml` | Builds and syncs to Bunny Storage, then purges the pull zone |

### Why so few jobs

GitHub bills **per job** and rounds every job up to a whole minute. Eight jobs
that finish in twenty seconds each cost eight minutes for two minutes of work,
and on a private repository that comes straight out of the 2,000 free minutes.
This template used to have eight per push; it has three.

Nothing was dropped. The same linters, the same rules, the same files:

- **The site jobs are merged.** The build, HTMLHint and lychee sat on three
  runners with three Hugo setups. Now one. The unminified build for HTMLHint
  goes to `src/public-lint/` so lychee keeps the real output, and it does not
  reprocess the images: `resources/_gen` is already warm from the first build.
  The artifact between build and link-check is gone, and with it the upload,
  the download and the storage.
- **zizmor moved** from `security.yml` into the repo job. It lints the same
  files as actionlint, only on security rather than syntax.
- **Scorecard runs weekly and on `main`**, not on every pull request. It rates
  branch protection, pinned dependencies and code review, and none of that
  changes per commit.
- **`concurrency` with `cancel-in-progress`** on both workflows, except on
  `main`. Pushing three times to the same PR now leaves one run standing
  instead of three.

Inside the repo job every step runs on `!cancelled()`, so one red linter does
not hide the others. The job still fails as soon as anything is wrong.

### Dependency updates

There is no `package.json`. Renovate keeps GitHub Actions current on its own,
and picks up tool versions from the `# renovate:` comment above each one.

Renovate cannot compute a checksum, so a version bump would otherwise land with
the previous release's hash still in place and fail the build.
`update-checksums.yml` recalculates them on Renovate's own pull requests and
commits the result back. It verifies each download against the checksum the
project publishes before writing anything, so a hash only lands here if
upstream vouches for it too.

That flow depends on `gitIgnoredAuthors` in `renovate.json`. Without it Renovate
treats the bot's commit as the branch having been modified by someone else and
stops maintaining the pull request.

To bump a tool by hand:

```bash
.github/scripts/update-tool-checksums.sh
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

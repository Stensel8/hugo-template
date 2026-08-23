# Contributing

Found a bug, have an improvement in mind, or want to extend the template? Issues and Pull Requests are welcome!

---

## Commit messages

This project uses [Conventional Commits](https://www.conventionalcommits.org/).

**Format:**

```
<type>: <short description>
```

**Types:**

| Type | When to use |
|------|-------------|
| `feat` | New layout, component, or template feature |
| `fix` | Bug fix — broken layout, incorrect config, rendering issue |
| `docs` | Changes to README, CONTRIBUTING, or other meta files |
| `chore` | Maintenance — dependencies, CI/CD, config |
| `style` | Formatting, whitespace, typo fixes |
| `refactor` | Restructure without changing behavior (e.g. rename files, move sections) |
| `content` | Update or improve existing page content |
| `revert` | Reverting a previous commit |

**Examples:**

```
feat: add dark mode toggle component
fix: correct baseURL placeholder in hugo.toml
docs: update usage instructions for src/ layout
chore: upgrade renovate config to v7
style: fix trailing whitespace in baseof.html
```

**Rules:**

- Use lowercase for the type and description
- Keep the subject line under 72 characters
- No period at the end
- Use the imperative mood ("add", "fix", "update" — not "added", "fixed", "updated")

---

## Pull requests

- PR titles must follow the same commit convention above
- One logical change per PR
- Test locally with `cd src && hugo server` before opening a PR
- Target the `main` branch

---

## Local development

```bash
git clone https://github.com/THectic-NL/hugo-template.git
cd hugo-template/src
hugo server
```

Hugo serves the site at `http://localhost:1313` by default.

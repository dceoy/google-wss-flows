# Repository Guidelines

## Project Structure & Module Organization

This repository is intentionally small and content-focused.

- `README.md`: high-level project description.
- `prompts/`: reusable prompt templates, currently `daily-news-headlines.prompt.md` and `daily-analyze-market-news.md`.
- `.github/workflows/ci.yml`: CI definition (shell/workflow linting and Dependabot auto-merge flow).
- `.agents/skills/`: local agent skills and scripts used for maintenance tasks (for example local QA).

Keep new prompt assets in `prompts/` and use clear, purpose-based names such as `topic-name.prompt.md`.

## Build, Test, and Development Commands

There is no application build step yet. Use QA/lint commands to validate changes:

- `./.agents/skills/local-qa/scripts/qa.sh`: runs full local QA (ShellCheck, Prettier, zizmor, actionlint, yamllint, checkov).
- `npx prettier --write './**/*.md'`: formats Markdown files.
- `actionlint .github/workflows/*.yml`: validates GitHub Actions workflows.

Run QA before opening a pull request.

## Coding Style & Naming Conventions

- Markdown: keep headings hierarchical and language precise; prefer short sections and bullets.
- Indentation: use 2 spaces in YAML and 2 spaces in Markdown nested lists.
- Filenames: use lowercase kebab-case for prompts and docs (example: `daily-news-headlines.prompt.md`).
- Keep prompt instructions explicit, testable, and free of contradictory requirements.

## Testing Guidelines

This repo currently relies on static QA rather than runtime tests.

- Treat `qa.sh` as the required validation suite.
- Ensure CI passes on `main`-targeted pull requests.
- If executable code is added later, include corresponding tests in a dedicated `tests/` directory and document how to run them in `README.md`.

## Commit & Pull Request Guidelines

- Commit messages in this repo follow concise imperative style (examples: `Remove ...`, `Format ...`, `Initial commit`).
- Prefer one logical change per commit.
- PRs should include:
  - brief summary of what changed and why,
  - linked issue (if applicable),
  - sample output or screenshots only when UI/rendered formatting changes.
- Confirm local QA results in the PR description.

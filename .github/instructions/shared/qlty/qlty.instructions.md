---
applyTo: "**"
---

<!-- Synced from zencq/.github (instructions/qlty/). Edit it there; changes made in a consuming repository are overwritten. -->

# Qlty

- The Qlty configuration (`.qlty/qlty.toml`, `.qlty/configs/`) is synced from `zencq/.github`: edit it there.
- A repository that needs its own Qlty settings (such as `exclude_patterns`) keeps `.qlty/qlty.toml` as its own: the sync creates it once and replaces it only when started by hand with that option, so carry the repository's additions over then. Its own instructions say so.
- Qlty lints the workflows, Markdown, `.editorconfig` compliance, and secrets, and finds duplication and complexity in the code. It has no linter for the code's language; that is the job of the language's own tools (see `commands.instructions.md`). Tests live in `tests/`, which `test_patterns` in `.qlty/qlty.toml` expects.
- Install the Qlty CLI from [the Qlty docs](https://docs.qlty.sh/cli/quickstart#install-the-cli) if `qlty` isn't available. Before finishing, run these and fix what they report:

  ```sh
  qlty check --fix --level=low                                           # changed files
  qlty smells                                                            # duplication and complexity in changed files
  ```

- For the whole repository, as Qlty Cloud checks on every push:

  ```sh
  qlty check --all --level=low
  qlty smells --all
  ```

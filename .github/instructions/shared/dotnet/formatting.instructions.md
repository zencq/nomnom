---
applyTo: "**"
---

<!-- Synced from zencq/.github (instructions/dotnet/). Edit it there; changes made in a consuming repository are overwritten. -->

# Formatting and linting

- `.editorconfig`, `.gitattributes`, and the Qlty configuration (`.qlty/qlty.toml`, `.qlty/configs/`) are synced from `zencq/.github` as well: edit them there.
- A repository that needs its own Qlty settings (such as `exclude_patterns`) keeps `.qlty/qlty.toml` as its own: the sync creates it once and replaces it only when started by hand with that option, so carry the repository's additions over then. Its own instructions say so.
- The rules live in `.editorconfig`: LF line endings on every OS (enforced for commits by `.gitattributes`), 4-space indentation in `.cs` files, and 2 spaces in csproj/props/json/md files.
- The spell-checker dictionary is `.exclusion.dic`; add the domain words it flags there.
- Run `dotnet format` before committing (see `commands.instructions.md`); the build doesn't flag whitespace, so CI checks it with `dotnet format --verify-no-changes`. The naming rules are only suggestions that no check enforces, so follow them anyway.
- Qlty (`.qlty/qlty.toml`) lints the workflows, Markdown, `.editorconfig` compliance, and secrets; it has no C# linter. Install the Qlty CLI from [the Qlty docs](https://docs.qlty.sh/cli/quickstart#install-the-cli) if `qlty` isn't available. Before finishing, run these and fix what they report:

  ```sh
  qlty check --fix --level=low                                           # changed files
  qlty smells                                                            # duplication and complexity in changed files
  ```

- For the whole repository, as Qlty Cloud checks on every push:

  ```sh
  qlty check --all --level=low
  qlty smells --all
  ```

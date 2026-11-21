---
applyTo: "**"
---

<!-- Synced from zencq/.github (instructions/dotnet/). Edit it there; changes made in a consuming repository are overwritten. -->

# Formatting and linting

- `.editorconfig` and `.gitattributes` are synced from `zencq/.github` as well: edit them there.
- The rules live in `.editorconfig`: LF line endings on every OS (enforced for commits by `.gitattributes`), 4-space indentation in `.cs` files, and 2 spaces in csproj/props/json/md files.
- The spell-checker dictionary is `.exclusion.dic`; add the domain words it flags there.
- Run `dotnet format` before committing (see `commands.instructions.md`); the build doesn't flag whitespace, so CI checks it with `dotnet format --verify-no-changes`. The naming rules are only suggestions that no check enforces, so follow them anyway.
- Qlty has no C# linter; see `qlty.instructions.md` for what it checks and the commands to run.

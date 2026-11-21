---
applyTo: ".github/instructions/**,.github/copilot-instructions.md,AGENTS.md,CLAUDE.md"
---

<!-- Synced from zencq/.github (instructions/common/). Edit it there; changes made in a consuming repository are overwritten. -->

# Authoring instructions

## Shared and repository files

- The rules every repository shares come from `zencq/.github`, which syncs them by pull request into `.github/instructions/shared/` (one folder per layer, such as `common/` for every repository and `dotnet/` for every .NET repository; `docs/README.md` in `zencq/.github` lists them). Never edit them in the repository they are synced to; change them in `zencq/.github` instead.
- Shared files hold no repository-specific names: no types, files, paths, or solution names of any one repository. Examples use neutral, made-up names (such as `OrderTotal` or `MAX_RETRY_COUNT`).
- The repository's own files live directly in `.github/instructions/`. They may add to a shared topic (for example the repository's current target frameworks, or an example from its own code), but never override or contradict a shared rule. If a shared rule doesn't fit a repository, change it in `zencq/.github`.
- Every repository has a `commands.instructions.md` with its own commands (such as build, format, test, and pack); shared files refer to it by name.

## Files

- Each file covers one concern and is named `<topic>.instructions.md`. Try to keep `<topic>` a single lowercase word (for example `tests.instructions.md`).
- Every file starts with YAML frontmatter that has an `applyTo` key, before anything else, followed by a `#` title. Use `##` sections when a file has more than one group of rules.
- `applyTo` is a single string. Use the narrowest glob that fits, and separate several globs with commas (`"**/*.csproj,**/*.props"`). Use `"**"` only for rules every task needs. A glob without `**/` (such as `"*.cs"`) matches only files in the repository root.
- Add `excludeAgent` (`"code-review"` or `"cloud-agent"`) only when a file must not reach one of the Copilot agents.

## Content

- Write the desired state, not legacy behavior or planned changes. A rule that names what to track, such as "the latest GA SDK", stays true on its own; a list of current values (such as the target frameworks) changes only when the repository does.
- State each fact in exactly one file. Reference another file by name (`see commands.instructions.md`) instead of repeating it.
- Put a fact in the file whose `applyTo` matches where it matters: rules for `.cs` files go in a file for `**/*.cs`, not in a repository-wide file.
- Keep general rules apart from the current state (for example, the package structure versus the packages that exist today), so adding a package changes as few lines as possible.
- Write short, concrete rules. Leave out generic best practices and anything an agent can read straight from the code. Include examples only when they clarify a non-obvious rule.
- Verify every path, command, and setting against the repository before writing it.
- Write paths repo-relative in backticks. Put commands in fenced `sh` blocks that can be copied as they are.

## Maintenance

- Update the instructions in the same commit as a change that makes them wrong, and remove outdated guidance right away. For a shared rule, open the change in `zencq/.github` as well.
- Treat these files as living guidance. When recurring requests or repeated corrections from the user show a stable preference or workflow rule, add it as an explicit rule without waiting to be asked, and say so in your reply.
- Capture repeated mistakes as explicit rules so they are less likely to recur.

## Entry points

- `CLAUDE.md`, `AGENTS.md`, and `.github/copilot-instructions.md` hold no rules; they only point to `.github/instructions/`.
- Each layer in `.github/instructions/shared/` has a `README.md` index that lists its files with what they apply to, each as an `@` import. It is generated in `zencq/.github` and synced with the layer, so a shared file added, renamed, or removed needs no change in the repositories.
- `AGENTS.md` lists each layer the repository gets by the `@` path of its index (`@.github/instructions/shared/common/README.md`), then the repository's own files in a table, each as an `@` path with what it applies to. When one of the repository's own files is added, renamed, or removed, or a layer comes or goes, update that list.
- `CLAUDE.md` holds only `@AGENTS.md`: Claude Code follows the imports through `AGENTS.md` and the indexes to every file. Tools that add their own blocks to `AGENTS.md` (between `<!-- name:start -->` and `<!-- name:end -->` markers) keep them below the hand-written part; don't edit those blocks.
- The tools fix their blocks' style themselves, so the hand-written part of `AGENTS.md` ends with a comment that says so and `<!-- markdownlint-disable -->`, which turns off every markdownlint rule for the blocks below it, whichever tool wrote them. markdownlint keeps checking the hand-written part above it.
- Agents load the files differently: Claude Code imports all of them, Copilot loads the ones whose `applyTo` matches, and other agents read `AGENTS.md` and follow its paths. Each file must therefore make sense on its own.

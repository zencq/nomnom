---
applyTo: "**"
---

<!-- Synced from zencq/.github (instructions/common/). Edit it there; changes made in a consuming repository are overwritten. -->

# Dependabot

- Every repository has a `.github/dependabot.yml` with an entry for each package ecosystem Dependabot supports in it: `github-actions` for the workflows, and the package manager of each language or tool the repository uses (such as `nuget`, which also covers `.config/dotnet-tools.json`, `npm`, `pip`, or `docker`). A change that adds an ecosystem adds its entry in the same commit.
- Leave out an ecosystem only when Dependabot has nothing useful to update, and say why in a comment in the file (for example, a `Dockerfile` that names only a major version already gets the latest release with each build).
- Each entry checks `weekly`. Group all GitHub Actions updates into one pull request, and the minor and patch updates of a package manager into another; major updates come one at a time, since they may need code changes.
- Set `commit-message.prefix` so the commits follow Conventional Commits (see `commits.instructions.md`): `ci` for GitHub Actions, and `deps` for the dependencies that ship with the repository, since release-please releases `deps` commits. Where the ecosystem tells development dependencies apart, give them `prefix-development: "chore"` so they don't create a release.

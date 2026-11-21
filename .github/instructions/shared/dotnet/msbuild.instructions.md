---
applyTo: "**/*.csproj,**/*.props,**/packages.lock.json,nuget.config"
---

<!-- Synced from zencq/.github (instructions/dotnet/). Edit it there; changes made in a consuming repository are overwritten. -->

# Project files and dependencies

- Shared settings live in `Directory.Build.props` and apply to every project; put new shared settings there rather than in a csproj.
- Package versions are managed centrally in `Directory.Packages.props`, so `PackageReference` entries must not have a `Version`.
- Every project uses `packages.lock.json` (`RestorePackagesWithLockFile` in `Directory.Build.props`); commit lock-file updates whenever dependencies change. Don't enable `RestoreLockedMode`: the lock files also pin packages the SDK adds implicitly (such as `Microsoft.NET.ILLink.Tasks`), whose versions follow the installed SDK, and CI always installs the latest one.
- `nuget.config` clears the global package sources and lists nuget.org, so extra sources on a machine can't fail restore with NU1507.
- A repository that uses zencq packages from GitHub Packages adds the source `github.zencq` (`https://nuget.pkg.github.com/zencq/index.json`) with the username `zencq` and the password `%NUGET_GITHUB_TOKEN%`, and package source mapping that sends only those packages there and everything else to nuget.org. The token is `GITHUB_TOKEN` in the workflows, whose restoring jobs need `packages: read`, and a personal access token with `read:packages` locally. `GITHUB_TOKEN` reads a package of another repository only if that package grants the consuming repository access under **Manage Actions access** in its settings.
- Keep external dependencies minimal and justified; their licenses must fit the repository's (see `license.instructions.md`).

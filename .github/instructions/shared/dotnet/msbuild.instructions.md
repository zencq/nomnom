---
applyTo: "**/*.csproj,**/*.props,**/packages.lock.json,nuget.config"
---

<!-- Synced from zencq/.github (instructions/dotnet/). Edit it there; changes made in a consuming repository are overwritten. -->

# Project files and dependencies

- Shared settings live in `Directory.Build.props` and apply to every project; put new shared settings there rather than in a csproj.
- Package versions are managed centrally in `Directory.Packages.props`, so `PackageReference` entries must not have a `Version`.
- Every project uses `packages.lock.json` (`RestorePackagesWithLockFile` in `Directory.Build.props`); commit lock-file updates whenever dependencies change. Don't enable `RestoreLockedMode`: the lock files also pin packages the SDK adds implicitly (such as `Microsoft.NET.ILLink.Tasks`), whose versions follow the installed SDK, and CI always installs the latest one.
- `nuget.config` limits restore to nuget.org; without it, extra global sources can fail restore with NU1507.
- Keep external dependencies minimal and justified. Dependencies and any code taken from elsewhere must have a license compatible with the repository's license.

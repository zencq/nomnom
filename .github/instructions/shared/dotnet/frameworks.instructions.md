---
applyTo: "**"
---

<!-- Synced from zencq/.github (instructions/dotnet/). Edit it there; changes made in a consuming repository are overwritten. -->

# Target frameworks

- Support every .NET release, LTS and STS alike, until one year after its [official end of support](https://dotnet.microsoft.com/platform/support/policy/dotnet-core). Add a new release as soon as it is GA.
- Target frameworks are set once in `Directory.Build.props` and apply to every project, tests included. Each repository lists the current target frameworks and the places to update with them in its own instructions.
- APIs newer than the oldest target framework need a fallback for the older targets.
- Each repository says in its own instructions which .NET SDK it builds with, unless a shared rule already does (as for NuGet libraries).

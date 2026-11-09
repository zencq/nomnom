---
applyTo: "**"
---

<!-- Synced from zencq/.github (instructions/dotnet/). Edit it there; changes made in a consuming repository are overwritten. -->

# Commits

- Commits follow Conventional Commits (`feat:`, `fix:`, `docs:`, `ci:` ...), because they drive version bumps and the changelog. Keep each commit to one coherent change that a single type fits.
- In a repository with several packages or projects, a change to one of them uses its name as scope, in lowercase (`feat(orders):`, `fix(billing):`). Repository-wide changes don't need a scope (`ci:`, `docs:`, `chore:`).
- Mark a breaking change with `!` after the type or scope (`feat(orders)!:`).

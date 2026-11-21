---
applyTo: "**"
---

<!-- Synced from zencq/.github (instructions/common/). Edit it there; changes made in a consuming repository are overwritten. -->

# Scope of changes

- Keep changes small and focused, and avoid broad refactors when a local fix is sufficient. Small improvements in the code you're already touching are fine along the way (a clearer name, an extracted method, an outdated comment).
- If an attempted fix doesn't work, revert it before trying a different one, so failed attempts don't pile up in the change.
- A change that adds a feature or changes behavior updates the documentation with it: the developer documentation in `docs/`, and for an app with an end-user wiki, the wiki pages as well. The repository's own instructions say where its wiki lives.

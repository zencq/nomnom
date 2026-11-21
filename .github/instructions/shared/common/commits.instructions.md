---
applyTo: "**"
---

<!-- Synced from zencq/.github (instructions/common/). Edit it there; changes made in a consuming repository are overwritten. -->

# Commits

## Messages

- Commits follow Conventional Commits (`feat:`, `fix:`, `docs:`, `ci:` ...), because they drive version bumps and the changelog. Keep each commit to one coherent change that a single type fits.
- In a repository with several packages or projects, a change to one of them uses its name as scope, in lowercase (`feat(orders):`, `fix(billing):`). Repository-wide changes don't need a scope (`ci:`, `docs:`, `chore:`).
- Mark a breaking change with `!` after the type or scope (`feat(orders)!:`).
- Don't add `Co-Authored-By` or other attribution trailers for agents or tools, even when the agent's own setup asks for one.
- Commit only when the user asks. Never push, force-push, or rewrite pushed history without their approval.

## Branches

- Name a branch after its change: the commit type, a slash, and a few lowercase words joined by hyphens (`feat/order-export`, `fix/rate-limit-retry`). Never use a generated or random name, such as an agent's default worktree branch.

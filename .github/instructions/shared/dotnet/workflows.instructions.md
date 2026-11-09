---
applyTo: ".github/workflows/**"
---

<!-- Synced from zencq/.github (instructions/dotnet/). Edit it there; changes made in a consuming repository are overwritten. -->

# GitHub Actions workflows

- Define `permissions` on each job, never at the workflow level, and grant only what that job needs.
- Pin every action to a full commit SHA with its version as a comment: `uses: actions/checkout@3d3c42e5aac5ba805825da76410c181273ba90b1 # v7.0.1`. The repository settings enforce SHA pinning, and Dependabot (`.github/dependabot.yml`) updates the SHA and the comment together.
- Give every job a `timeout-minutes` well above its usual run time, so a hung step doesn't block a runner for GitHub's six-hour default.
- Set `concurrency` on each workflow: CI cancels a run that a newer push to the same ref made outdated, while a workflow that publishes something (a release, a deployment) queues its runs and never cancels one, so nothing is left half-published.

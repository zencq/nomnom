---
applyTo: "**"
---

<!-- Synced from zencq/.github (instructions/common/). Edit it there; changes made in a consuming repository are overwritten. -->

# License

- Every repository has a `LICENSE` at its root, with the license chosen for that repository. GitHub can't take it from `zencq/.github` as a default, so a new repository adds its own.
- Everything a repository releases ships a copy of that `LICENSE`: a library with each package, next to its project file, and an image next to the application in its file system, with the license's SPDX identifier in the label `org.opencontainers.image.licenses`.
- When some files aren't covered by `LICENSE` (an adapted or vendored file, fonts, icons, or other assets), the README has a `## License` section that names `LICENSE` and lists each exception with its license. Without exceptions, leave the section out: GitHub shows the license from `LICENSE`.
- Dependencies and any code taken from elsewhere must have a license compatible with the repository's license.

# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-09-24

### Breaking

- The action now runs on the **Node 24** JavaScript runtime (`runs.using: node24`) instead of Node 20. Self-hosted runners must be **v2.327.1 or newer**. macOS 13.4 and older, and ARM32 self-hosted runners, are not supported. `1.0.19` and earlier still use Node 20, which GitHub removed from Actions runners on 2026-09-23.

### Added

- Non-PR/push workflows now publish the package and write a job summary with the commit install URL, instead of failing with "This action is only supported for pull requests."

### Changed

- Full rebrand from try-module.cloud to pkg.vc (action name, repository, client library, and PR comment identifiers).
- Build with Bun: source is now `index.ts`, bundled to `dist/index.js` (replaces Rolldown + `index.js`).
- Dependencies: `pkg.vc` `^1.0.2` (replaces `try-module.cloud`) and `dedent` `^1.7.0`.

### Fixed

- Job summary headings now interpolate the package name (they previously rendered the literal `${package_name}`).

[2.0.0]: https://github.com/pkg-vc/publish-action/compare/1.0.19...2.0.0

# Mooring's SwiftGitX

[SwiftGitX](https://github.com/ibrahimcetin/SwiftGitX) for
[Mooring](https://mooring.sh). The only change from upstream is **which libgit2
it builds against**.

Upstream SwiftGitX pins `ibrahimcetin/libgit2` with `exact: "1.9.2"`, and that
fork stopped short of the libgit2 1.9.5 security release (CVE-2026-53586,
CVE-2026-53587). An `exact:` pin in a dependency cannot be overridden from the
app that uses it, so moving libgit2 meant moving SwiftGitX too. This fork pins
[mooring-sh/libgit2](https://github.com/mooring-sh/libgit2) instead; how that
one is built, and why its feature macros need care, is in its `MOORING.md`.

| Tag | Upstream base | libgit2 |
|---|---|---|
| `0.4.1` | `0.4.0` | mooring-sh/libgit2 `1.9.7` |

## Changes on top of upstream

- `Package.swift`: the libgit2 dependency URL and version.
- `Tests/SwiftGitXTests/SwiftGitXTests.swift`: the libgit2 version it expects.

## Bumping libgit2

Change the `exact:` pin, then run `swift test` and compare the list of failing
tests with a run of the previous tag. On a developer Mac about 30 tests fail on
both, because they depend on the machine's git config (default branch name,
stash messages). Only a difference between the two runs counts. Then tag the
next patch version and bump Mooring's pin.

---
name: dagsec
description: Check npm, PyPI and crates.io packages with dagsec before adding, upgrading or recommending them. Use whenever a dependency is added to package.json, requirements.txt, pyproject.toml or Cargo.toml, when choosing between libraries, or when an install is blocked by dagsec.
---

# Checking dependencies with dagsec

dagsec knows about vulnerabilities published after your training data, so its answer overrides what you remember about a package's safe versions.

## Before adding or upgrading a dependency

1. Call the `check_package` tool from the `dagsec` MCP server with the package `name`, its `ecosystem` (`npm`, `pypi` or `crates`) and, if you intend to pin one, the exact `version`.
2. Act on the first line of the result:
   - **DO NOT INSTALL**: the package doesn't exist. Don't guess a similar name; ask the user which package they meant.
   - **DO NOT USE name@version**: install the version it recommends instead, and tell the user why in one sentence.
   - **RISKY**: the package is poorly maintained. Tell the user and suggest a well-maintained alternative before installing.
   - **OK** or **OK WITH CAUTION**: go ahead.
3. When editing a manifest by hand (not through an install command), check each new package the same way. The install hook only sees install commands.

## When an install is blocked

The dagsec hook stops `npm install`, `pip install`, `cargo add` and similar commands when a package doesn't exist or the version has critical or high vulnerabilities. The block message names the safe version. Rerun the install with that version. Don't work around the block by editing lockfiles or using another package manager.

If the user explicitly wants the vulnerable version (for example to reproduce a bug), explain the risk and let them run the command themselves.

# dagsec for Claude Code

AI coding agents install packages from memory: versions that were safe when they were trained, and sometimes names that don't exist at all. This plugin puts [dagsec](https://dagsec.net) between Claude Code and your package manager.

- **Blocks risky installs.** Before `npm install`, `pip install`, `cargo add`, `go get`, `dotnet add package` and similar commands run, dagsec checks each package. A package that doesn't exist, or a version with critical or high vulnerabilities, is stopped and Claude is told which version to use instead.
- **Answers "is this package safe?"** Claude can check any npm, PyPI, crates.io, Go, Maven or NuGet package: known vulnerabilities for a version, the release that fixes them, and a 0 to 100 health score.

## Install

1. Create an API key at [app.dagsec.net/keys](https://app.dagsec.net/keys).
2. In Claude Code:

```
/plugin marketplace add hasanerman/dagsec-claude
/plugin install dagsec@dagsec
```

3. Paste your API key when asked. Leave **mode** as `block` to stop risky installs, or set it to `warn` to be asked first.

## What is sent to dagsec

Only install commands (such as `npm install axios`) and the package names and versions Claude checks. Your code never leaves your machine, and other shell commands are never sent.

## Plans

Every plan includes agent checks: 500 a month on Free, 20,000 on Pro and 200,000 on Team. See [dagsec.net](https://dagsec.net/#pricing). When the monthly checks run out, installs are no longer checked; they are not blocked.

---

© 2026 dagsec. All rights reserved. This repository contains only the plugin definition; the dagsec service is proprietary.

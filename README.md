# charity_ransomware_v1

> **⚠️ SAFETY & ETHICS NOTICE — READ BEFORE PROCEEDING ⚠️**
>
> This repository's name and description reference "ransomware". Any work in this repository is intended **strictly for educational and security-research purposes only**.
>
> - **Do NOT run any payload code on any machine you care about.**
> - **Do NOT run any payload code outside of an isolated, disposable environment** (e.g., an offline VM with snapshots, a sandboxed container).
> - **Restrict or disable network access** in any environment where this code runs.
> - **Never test against real user data, production systems, or cloud infrastructure.**
> - Misuse of ransomware-style techniques may be **illegal** and is always **unethical**.
>
> The maintainers of this repository accept no liability for misuse. If you discover a genuine security concern, please open a private security advisory rather than a public issue.

---

## Table of Contents

1. [What is this project?](#what-is-this-project)
2. [Current Status](#current-status)
3. [Safety & Ethics Notice](#safety--ethics-notice)
4. [Repository Structure](#repository-structure)
5. [Prerequisites](#prerequisites)
6. [Safe Inspection & Testing Steps](#safe-inspection--testing-steps)
7. [Remote Testing via GitHub Actions](#remote-testing-via-github-actions)
8. [Contributing](#contributing)
9. [Troubleshooting & FAQ](#troubleshooting--faq)
10. [License](#license)

---

## What is this project?

`charity_ransomware_v1` is an **experimental, prototype-stage** research project created to explore the technical viability of ransomware-style mechanisms (file encryption, key management, ransom-note delivery, etc.) in the context of charity / awareness campaigns.

The original repository description is: *"check to see how viable this is".*

The stated goal is research and education — to understand how such software is built so that defenders, researchers, and educators can better detect, explain, and mitigate similar real-world threats.

**This is not production software.** It should never be deployed against real systems or real users.

---

## Current Status

| Area | Status |
|------|--------|
| Core payload logic | 🚧 Not yet implemented |
| Key-management module | 🚧 Not yet implemented |
| Ransom-note template | 🚧 Not yet implemented |
| Decryption / recovery tool | 🚧 Not yet implemented |
| Unit tests | 🚧 Not yet implemented |
| CI / GitHub Actions smoke test | 🔄 In progress (see [PR #3](../../pull/3)) |
| Documentation | ✅ This README |

The repository is in its earliest possible stage. Only a stub README exists on the `master` branch. All substantive code is **TODO**.

---

## Safety & Ethics Notice

Because of the sensitive nature of this project, the following guidelines apply to **all contributors and users**:

### Allowed use
- Reading, reviewing, and understanding the code for educational purposes.
- Running **static analysis** (linters, type-checkers) that do not execute the core payload.
- Running **unit tests** that use mock/fake file systems and never touch real files.
- CI pipelines on GitHub-hosted runners (ephemeral, controlled environments).

### Not allowed
- Running payload code on any non-disposable machine or VM.
- Pointing the tool at real files, real users, or live cloud infrastructure.
- Distributing compiled binaries derived from this repository without prominent safety warnings.
- Using techniques from this project to target anyone without their explicit written consent.

### Safe environment checklist
Before doing *any* execution:

- [ ] Use a **disposable VM or container** (e.g., VirtualBox snapshot, Docker with `--read-only` root FS).
- [ ] **Disable or sandbox network access** (e.g., `--network none` in Docker, host-only adapter in VirtualBox).
- [ ] **Snapshot the VM before running** so you can roll back instantly.
- [ ] Work only with **dummy / synthetic data** — no personal files, credentials, or sensitive documents.
- [ ] Review all code changes before executing them.

---

## Repository Structure

```
charity_ransomware_v1/
├── .github/
│   └── workflows/
│       └── ci.yml          # (planned) Safe GitHub Actions smoke-test workflow
├── README.md               # This file
```

> **Note:** The repository currently contains only this README. All other directories and files listed above are planned or in progress. As code is added, this section will be updated to reflect actual contents.

**Planned structure** (subject to change):

```
charity_ransomware_v1/
├── .github/
│   └── workflows/
│       └── ci.yml          # Safe CI smoke-test (lint/static checks only)
├── scripts/
│   └── ci/
│       └── detect_language.sh  # Language/tooling detection helper for CI
├── src/                    # Core source code (TODO)
├── tests/                  # Unit tests using mock file systems (TODO)
├── docs/                   # Extended documentation (TODO)
└── README.md
```

---

## Prerequisites

> ⚠️ **Do not attempt to run any code from this repository until it has been implemented and reviewed, and then only in a safe isolated environment (see [Safety & Ethics Notice](#safety--ethics-notice)).**

Once code is implemented, prerequisites will be listed here. Expected items include:

- A supported language runtime (TBD — Python 3.x / Node.js / other).
- Any language-specific package manager (`pip`, `npm`, etc.).
- A disposable VM or sandboxed container (mandatory).

---

## Safe Inspection & Testing Steps

Since the core code is not yet implemented, the safest and recommended approach is **static inspection only**:

1. **Browse code on GitHub** — use the GitHub web UI to read source files without downloading anything.
2. **Run linters / static analysis** — once code is added, linters (e.g., `flake8`, `eslint`) can check for issues without executing the payload.
3. **Use GitHub Actions** — trigger the CI workflow remotely; GitHub runs the checks on an ephemeral hosted runner, not on your machine (see next section).
4. **Open in GitHub Codespaces** (if enabled) — provides a browser-based VS Code environment isolated from your local machine.

---

## Remote Testing via GitHub Actions

The recommended way to validate this repository **without running anything locally** is to use the GitHub Actions CI workflow. A smoke-test workflow is being added in [PR #3](../../pull/3) and will be available on `master` once merged.

### What the workflow does
- Checks out the repository on a **GitHub-hosted ephemeral runner**.
- Detects the project language and tooling.
- Runs **static checks only** (lint, type-check, import validation) — it explicitly skips execution of any payload code.
- Prints a clear summary of what was detected, what ran, and what was skipped for safety.

### How to trigger manually (workflow_dispatch)

1. Go to the repository on GitHub and click the **"Actions"** tab at the top of the page.
2. In the left sidebar, click the workflow named **"CI Smoke Test"** (or similar — check the tab after PR #3 merges).
3. Click the **"Run workflow"** button (top-right of the workflow run list).
4. Select the branch you want to test (`master` or your feature branch).
5. Click **"Run workflow"** to confirm.

The workflow will appear in the list within a few seconds and will show a spinner while running.

### How to view logs

1. Click the workflow run in the list to open it.
2. Click a job name (e.g., **"smoke-test"**) to expand it.
3. Click any step to see its full log output.
4. Look for lines like:
   - `✅ Detected language: <language>` — what the runner found.
   - `⏭️  Skipping payload execution for safety` — confirms no destructive code ran.
   - `✅ Static checks passed` / `❌ Static checks failed` — the overall result.

### Interpreting results

| Result | Meaning |
|--------|---------|
| ✅ All steps green | Static checks pass; repository structure is valid. |
| ❌ A step failed | See the step log for details. Likely a lint error or missing file. |
| ⏭️  Step skipped | Intentionally skipped for safety (e.g., payload execution). |

### Automatic triggers

Once the workflow file is on `master`, it will also run automatically on:
- Every **push** to `master`.
- Every **pull request** targeting `master`.

---

## Contributing

Contributions are welcome, but given the sensitive nature of this project, please follow these additional guidelines beyond the standard GitHub workflow:

1. **Open an issue first** to discuss any new feature or change before writing code.
2. **Never add code that could cause harm** if accidentally run outside a sandbox. If you need to add payload-like code for research purposes, ensure it is clearly gated behind an explicit safety flag and documented.
3. **Add or update unit tests** for any new code. Tests must use mock/fake file systems and must never touch real files.
4. **Update this README** if you add new files, directories, or change the project's status.
5. **Follow the PR process**: fork → branch → PR against `master`. All PRs require at least one review before merging.

### Branch naming convention

```
feature/<short-description>
fix/<short-description>
docs/<short-description>
```

### Commit message style

```
<type>: <short summary>

Types: feat, fix, docs, test, ci, chore, refactor
```

---

## Troubleshooting & FAQ

**Q: Why is the repository almost empty?**
A: This project is in the earliest prototype stage. The description "check to see how viable this is" reflects that the maintainer is still assessing whether to build it. No payload code has been written yet.

**Q: Is it safe to clone this repository?**
A: Cloning a repository only downloads files — it does not execute any code. However, always review files before running anything. Currently there is no executable code in the repository.

**Q: The GitHub Actions workflow doesn't appear in the Actions tab.**
A: The workflow (from PR #3) may not have been merged to `master` yet. Check the open pull requests and either wait for the merge or test from the PR's branch directly by triggering the workflow on that branch.

**Q: Can I use this for a CTF / security course?**
A: Potentially yes, as long as you follow the safety guidelines above and comply with your event's or institution's rules. Always run in an isolated environment.

**Q: I found a security vulnerability in this repository.**
A: Please do **not** open a public issue. Use GitHub's [private security advisory](https://github.com/ti84plusprograms/charity_ransomware_v1/security/advisories/new) feature to report it confidentially.

**Q: Something in the CI workflow failed and I don't understand the log.**
A: Open an issue and paste the relevant log snippet. Include the workflow run URL.

---

## License

No license has been specified for this repository yet. Until a license is added, default copyright law applies — the code may not be reused, modified, or distributed without explicit permission from the repository owner.

> **TODO:** Add a `LICENSE` file (e.g., MIT or Apache 2.0 with additional usage restrictions given the sensitive nature of the project).


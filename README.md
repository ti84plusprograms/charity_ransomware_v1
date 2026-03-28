# charity_ransomware_v1

> **Status:** early-stage research / viability check

---

## Remote CI Smoke Test (no local setup required)

A safe, non-destructive GitHub Actions workflow is included so you can
validate the repository on a hosted runner **without downloading or running
anything locally**.

### What the workflow does

| Step | Description |
|------|-------------|
| Checkout | Clones the repo onto the ephemeral GitHub-hosted runner |
| Language detection | Identifies Python, Node.js, or "none" and logs the result |
| Static checks | Syntax/lint/type checks only — **zero execution of the main payload** |
| Tests | Runs the test suite *if* a `tests/` directory is present |
| Fallback smoke | Lists repo contents and validates entrypoint files when no language is detected |
| Summary | Prints what was detected, what ran, and confirms the payload was skipped |

> **Safety guarantee:** The workflow is hard-coded to skip any step that would
> execute `main.py`, `index.js`, or equivalent entry-points.  Only static
> analysis tools (py_compile, flake8, mypy, eslint, tsc) and isolated unit
> tests are ever invoked.

### How to trigger

**Automatic:** The workflow runs on every push and pull-request to `master`.

**Manual (from the GitHub UI):**

1. Go to the repository on GitHub.
2. Click the **Actions** tab.
3. Select **CI Smoke Test** from the left sidebar.
4. Click **Run workflow → Run workflow** (branch: `master`).

### How to interpret the results

* **Green ✓** — all static checks passed (or no source code found yet).
* **Red ✗** — a syntax/lint error was detected; click the failing job to read
  the log.
* The final **Summary** step always prints which language was detected, whether
  tests were found, and confirms `Payload executed: NO`.

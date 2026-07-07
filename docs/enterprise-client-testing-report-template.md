# Enterprise adoption — retest report (send back)

**Purpose:** Fill this in on the adoption laptop and **send to the A11y Studio coordinator** when you finish a test session. Keep a copy locally.

**Checklist you ran from:** [enterprise-client-testing.md](./enterprise-client-testing.md)

**Redact before sending:** internal hostnames, auth tokens, client IDs, employee names, full monorepo paths if policy requires.

---

## Session header

| Field | Value |
| --- | --- |
| **Date** | YYYY-MM-DD |
| **Tester** | name or team |
| **Extension version** | e.g. 1.0.5 Marketplace / 1.0.6 VSIX |
| **Phase** | Repo fixes only (A) / Part A gates (B) / Both |
| **Verdict** | PASS / PARTIAL / BLOCKED |

**One-line summary (paste into Slack/email subject):**

```
Adoption retest [PASS|PARTIAL|BLOCKED] — A11y Studio v____ — [repo ready | Part A X/4 | blocker: …]
```

---

## Scorecard

| Gate / item | Result | Owner if FAIL |
| --- | --- | --- |
| A1 `yarn a11y --list` | PASS / FAIL | repo |
| A2 auth.setup ESM | PASS / FAIL / N/A | repo |
| A3 Playwright project names | PASS / FAIL / N/A | repo |
| **1** Diagnose | PASS / FAIL | extension |
| **2** Spec discovery | PASS / FAIL | extension / repo |
| **3** Run flow tests | PASS / FAIL / ENV BLOCKED | extension / env |
| **4** Record flow | PASS / FAIL / ENV BLOCKED | extension / env |

**Part A score:** ___ / 4 gates pass (ENV BLOCKED counts separately — note below)

---

## Blockers (if any)

For each open blocker, one row:

| ID | Symptom | Extension or repo? | What you tried |
| --- | --- | --- | --- |
| 1 | | | |
| 2 | | | |

---

## Evidence (paste below)

### Terminal — `yarn a11y --list`

```
[paste]
```

### Diagnose output (Output → A11y Studio Flow Runner)

```
[paste — redact secrets and internal URLs]
```

### `flowRunner` block (`a11y-studio.json` only)

```json
[paste — redact baseUrl secrets if needed]
```

### Gate 3 / 4 notes (Run, Record, env)

```
[paste or "ENV BLOCKED — dev host unreachable"]
```

---

## Coordinator reply template (for you)

Copy when everything passes:

```
Adoption retest PASS — A11y Studio v[version].
Part A: 4/4 (or 3/4 + Gate N ENV BLOCKED).
Repo: yarn a11y --list OK.
Report attached: enterprise-client-testing-report-YYYY-MM-DD.md
```

Copy when blocked:

```
Adoption retest BLOCKED — A11y Studio v[version].
Part A: [N]/4. Repo list: [OK|FAIL].
Top blocker: [one sentence]. Owner: [extension|repo|env].
Report attached: enterprise-client-testing-report-YYYY-MM-DD.md
```

---

*Template version: 2026-07-07 · Maintainer updates via [a11ystudio/media](https://github.com/a11ystudio/media)*

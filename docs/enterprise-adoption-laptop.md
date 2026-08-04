# A11y Studio — enterprise adopt-existing laptop brief

## COPILOT — OPEN THIS URL (CURRENT 2026-08-04)

**GitHub (read here):** https://github.com/a11ystudio/media/blob/main/docs/enterprise-adoption-laptop.md  

**Raw (fetch / paste):** https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-adoption-laptop.md  

**Cache-bust fetch (prefer if page looks old):** https://cdn.jsdelivr.net/gh/a11ystudio/media@main/docs/enterprise-adoption-laptop.md  

**Do not change this URL.** If the page still says **1.0.23** / **1.0.22** / Gates (a)+(b) as the current todo, hard-refresh or use the raw / cache-bust link — this file was updated for **1.0.24**.

The human cannot paste long chat instructions into you. This GitHub page is the vendor's message to you **and** the shared script for **human + Copilot pair testing**.

### World product — not one client (read first)

**A11y Studio is a global product.** Named environments (`local`, `qa`, `staging`, `dev2`, …) come from **each repo’s** `a11y-studio.json` → `flowRunner.environments`. The product does **not** prefer any key. Marketplace behavior must stay valid for **any** team worldwide.

This brief is **pair-run protocol for one adoption laptop session**. Env keys below are **human-designated for this run only** — not product defaults.

**Install Marketplace `a11ystudio.a11y-studio` `1.0.24` only, then Reload Window**, before this smoke. Do **not** keep testing on **≤1.0.23** — skip straight to **1.0.24**.

### Client constraint (non-negotiable)

- **Marketplace only** — Extensions → A11y Studio → **1.0.24**. No VSIX sideload. No vendor-repo files. No build-from-main.
- Never write customer **org**, **repo**, **hostname**, **URL**, or **person** names in chat, Output excerpts, or the report block.
- Use only generic env **kinds** the human confirms (`local` / `qa` / `staging` / `other`), `app HTML` / `404` / `NoSuchKey`, generic path shapes (`tests/a11y/.auth/<profile>.json`).
- Never paste secrets, tokens, or storageState contents.

### Context you must keep straight

| Fact | Meaning for you |
| --- | --- |
| **Floor** | Marketplace **1.0.24** LIVE — re-prove **Section A** after vendor fixes (F1–F6 + `--project=`) |
| **Already CLOSED** | Gate **(a)** known-violation honesty · Gate **(b)** multi-env Run all deny-mismatch (**PASSED** on ≥1.0.21) — **do not** re-prove as the main todo |
| **Your job** | Pair run on the **customer monorepo** laptop only — not the vendor `a11y-studio` repo |
| **wcag-map.json** | **Not required in the customer repo.** Bundled in the Marketplace extension. |
| **Auth profile selected** | Injects Playwright **`storageState`** (saved cookies/session) — it does **not** type username/password into login form steps in a recorded spec |
| **Record flow** | **Not required** for Section A |
| **Do not claim** | “1.0.24 laptop-validated” or adopt-ready until **Section A overall: PASS** |

---

### Pair testing — who does what

| Role | Does |
| --- | --- |
| **Human** | Clicks panel rows, confirms URL in a browser, inserts/edits journey labels, reads Output with Copilot |
| **Copilot** | Confirms version **1.0.24**, guides GATE PATH, fills the report block, **never** pastes secrets, org, repo, or hostnames |
| **Together** | Finish **Section A** first; optional **Section B** after; stop on red URL |

**Goal (this revision):**

- **Section A (required gate)** — `keyboardTabJourney` via **correct API**; correct labels **pass**; wrong labels **fail** (not hollow); L2 shows fail in HTML matrix; panel opens from violations badge without crash.
- **Section B (optional catch-up)** — P1-11 panel friction checks (Confluence path, CLI vendor honesty, Why on disabled chips, ENV-FALLBACK).

---

### YOUR TODO NOW (2026-08-04) — Marketplace **1.0.24** · Section A gate

| # | Todo | Owner | Done when |
| --- | --- | --- | --- |
| **T1** | Confirm extension is **1.0.24** + **Reload Window** | Human + Copilot | Version verified — **not** ≤1.0.23 |
| **T2** | Flow package chosen; trusted workspace; healthy env URL (human designates) | Human | App HTML (not 404 / `NoSuchKey`) |
| **T3** | **A1** — API present; use **`customChecks: [A11yStudioChecks.keyboardTabJourney([...])]`** inside `checkA11y` options (never as 2nd arg alone) | Human + Copilot | No opaque `replace` crash; clear error if API misused |
| **T4** | **A2** — Run with **correct** focus labels → must **PASS** | Human + Copilot | Journey green; L1 axe may pass; L2 may pass or N/A if no contract |
| **T5** | **A3** — Wrong labels / reversed order → must **FAIL** (hollow green = FAIL); HTML matrix **L2 = fail** | Human + Copilot | Violations in Problems + L2 fail in report |
| **T6** | Click **“N flow violations”** status badge → Flow Runner panel opens (no “Could not open” / reload) | Human + Copilot | Panel opens |
| **T7** | **A4** (if dialog available) — `focusTrapActive` Tab + Shift+Tab | Human + Copilot | PASS or SKIP with reason |
| **T8** | Fill **report block** → return to vendor / [#303](https://github.com/a11ystudio/a11y-studio/issues/303) | Copilot | **Section A overall** decided |
| **T9** | Optional **Section B** only after A | Both | PARTIAL OK |

**Not your todo:** Re-running Gate (a)/(b) as the primary smoke · Expand-all · VSIX · vendor-repo coding · naming customer org/repo/hostname · treating unrelated locator timeouts as Section A FAIL.

**Adopt messaging:** **OFF** until human/maintainer promotes after **Section A PASS**.

---

## FINAL EXPECTATION — when is the required gate CLOSED?

**Section A overall = PASS** (and the gate may close) **only if all of the following are true:**

1. Extension details show **1.0.24** (Marketplace, after Reload).
2. **A1** — `keyboardTabJourney` runs via **correct** `checkA11y({ label, customChecks: [...] })` pattern (no crash).
3. **A2** — Correct labels → journey **passes** (no false fail on matching focus order).
4. **A3** — Wrong / reversed labels → journey **fails** with real findings (not hollow “0 violations”).
5. HTML component-audit matrix shows **L2 fail** (not `— skip`) when keyboard-tab-journey findings exist.
6. Status-bar **flow violations** badge opens Flow Runner without forcing Reload Window.

**A4** may be **SKIP** if no dialog is available — note why. A4 alone does **not** block gate close.

**Gate stays OPEN (FAIL)** if any of A1–A3 fail, if L2 stays skip while findings exist, or if the panel badge crashes.

After **Section A overall: PASS**, Copilot reports PASS on the report block and [#303](https://github.com/a11ystudio/a11y-studio/issues/303). Maintainer then decides adopt messaging / next steps — Copilot does **not** declare adopt-ready alone.

---

## CURRENT — Auth reminder (read once)

Selecting an **auth profile** in the panel = use this **`storageState`** file for the run.

It does **not** fill Username/Password fields if the **spec itself** clicks login controls. Session missing/stale/wrong-env → app shows login again. Prefer journeys that start **after** login via storageState, or a dedicated auth-setup recording.

---

## CURRENT — GATE PATH (do in order)

### Step 0 — Install (Marketplace only)

1. Extensions → **A11y Studio** → **1.0.24** (Marketplace — **no VSIX**).
2. Command Palette → **Developer: Reload Window**.
3. Confirm version on the Extensions detail page — must say **1.0.24**.

### Step 1 — Open Flow Runner

1. Activity Bar → **A11y Studio** → **Flow Runner**.
2. **Choose Flow package** = folder that owns `a11y-studio.json` and Flow specs.
3. Confirm panel shows Playwright / Diagnose / Verify rows (plumbing).

### Step 2 — URL health (hard stop if red)

1. Ask the human which Flow environment key is healthy for **this** session.
2. Select that environment. Skip keys the human marked dead.
3. Human opens the **same entry URL** in Chrome/Edge.
4. Verdict: **App HTML** → continue. **404** / **NoSuchKey** → **STOP**.
5. Copilot records only: env kind + health — **no hostname**.

### Step 3 — Section A (keyboard journey) — **required gate**

1. Page with a clear Tab order. Labels must match **live focus announcements** (human reads focus with Tab once; Copilot helps phrase tokens).
2. Insert checkpoint pack **`keyboard-tab-journey`**, **or** use this **only** pattern:

```ts
await checkA11y(
  page,
  {
    label: 'A2: keyboard tab journey - correct labels',
    customChecks: [
      A11yStudioChecks.keyboardTabJourney([
        /* human-confirmed focus labels in Tab order — examples only */
        'Skip to Main Content',
        'Home',
      ]),
    ],
  },
  { specFile: '…', line: 1 },
);
```

**Wrong (crashes / opaque error on ≤1.0.23; clear throw on 1.0.24):**

```ts
// DO NOT — second arg must be CheckA11yOptions with label + customChecks
await checkA11y(page, A11yStudioChecks.keyboardTabJourney(['…']), context);
```

3. **A2** — Correct labels → must **pass**.
4. **A3** — Reverse order **or** one nonsense label → must **fail**; open Flow HTML → **L2 keyboard** cell is **fail** (not `— skip`).
5. Click Problems / status **“N flow violations”** → Flow Runner opens.
6. **A4** (optional) Dialog + `A11yStudioChecks.focusTrapActive('<selector>')`.

**Optional config (not required for gate):** `flowRunner.playwrightProject` in `a11y-studio.json` to pass `--project=` when the repo has multiple Playwright projects.

### Step 4 — Section B (optional, after A)

| # | Check | Pass when |
| --- | --- | --- |
| B1 | Confluence Connect → mapping → Publish | Panel path works (no peer Settings trap) |
| B2 | VSIX-vendored Studio CLI | No false “install public npm `@a11ystudio/cli`” |
| B3 | Disabled Flow/Reports actions | Inline **Why · …** (not hover-only) |
| B4 | Named env with **no** URL | No silent localhost inherit; Run/Record gated with reason |

### Step 5 — Evidence

1. Fill **Copilot report block** below.
2. Prefer also commenting the same templates on vendor issue [#303](https://github.com/a11ystudio/a11y-studio/issues/303) if the human has access — **this media URL stays the Copilot bookmark**.

---

## CURRENT — If FAIL (triage together)

| Output signal | Owner | Next action |
| --- | --- | --- |
| Still on **≤1.0.23** | **install** | Update Marketplace to **1.0.24** + Reload — retest invalid until then |
| Brief still says **1.0.23** as floor / Gates (a)+(b) as current | **stale cache** | Refetch raw / cache-bust URL above |
| URL / 404 / `NoSuchKey` | **environment** | Stop; env owners fix URL |
| `Cannot read properties of undefined (reading 'replace')` | **install / API** | Must be on **1.0.24** + use `customChecks: []` wrapper |
| A3 still **passes** with wrong labels | **product** | Hollow success — escalate (blocker) |
| L2 shows `— skip` but findings exist | **product** | Escalate (1.0.24 should map keyboard customs to L2) |
| Badge → “Could not open Flow Runner” | **product** | Escalate (fixed on 1.0.24 — retest after update) |
| Spec timeout on login `getByTestId` / username | **spec / app** | Not Section A — fix journey or storageState |
| Expand all broken | **vendor-roadmap** | Skip |

Do **not** use public sauce-demo as a substitute for this adoption repo.

---

## Document revision

**Document revision:** **2026-08-04** · **Supersedes all earlier versions of this URL**  
**GitHub:** https://github.com/a11ystudio/media/blob/main/docs/enterprise-adoption-laptop.md  
**Canonical raw:** https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-adoption-laptop.md  

| Field | Value |
| --- | --- |
| **This revision** | **2026-08-04** — Marketplace **1.0.24**; Section **A** required gate (API + A2/A3 + L2 + panel badge); Section **B** optional |
| **Marketplace floor** | **v1.0.24** LIVE |
| **Copilot workspace** | **Customer monorepo only** |
| **Naming** | Reports stay **neutral** — no customer org, repo, hostname, or project codenames |
| **URL** | **Unchanged** — same media path Copilot already bookmarks |

### How to read this page (anti-stale)

1. Confirm **Document revision** is **2026-08-04** (or newer) and floor **v1.0.24**. If brief still says **1.0.23** or **1.0.18**, refetch raw URL (hard refresh / cache-bust).
2. Only sections marked **CURRENT** are actionable. **YOUR TODO NOW** + **GATE PATH** + **FINAL EXPECTATION** are the priority.
3. Sections marked **HISTORICAL** are context only.
4. If two bullets disagree, the **newer dated** block wins.

### Install (CURRENT)

**Extension:** Marketplace **`a11ystudio.a11y-studio` `1.0.24`**

1. Extensions → A11y Studio → update to **1.0.24**.
2. **Developer: Reload Window**.
3. Confirm version in Extensions detail.

### Shipped focus for this laptop (1.0.24)

| Item | Why it matters |
| --- | --- |
| **`keyboardTabJourney` API guard** | Wrong usage throws a clear error instead of crashing the panel |
| **L2 matrix mapping** | Keyboard custom findings show as L2 fail (not skip) |
| **Violations badge → panel** | Opens Flow Runner without reload |
| **`flowRunner.playwrightProject`** | Optional `--project=` for multi-project Playwright configs |
| **Guided checks HTML** | Collapsed / relevant-only by default (less report noise) |
| **Env filter (already LIVE)** | Gate (b) closed — not the primary todo |

### Known deferred / out of scope

| Item | Status |
| --- | --- |
| Re-prove Gate (a)/(b) as main smoke | **CLOSED** — optional sanity only |
| Expand all | Skip if broken |
| L3 visual · Figma · Docker product · adopt media | HOLD until Section A PASS + maintainer promote |

### CURRENT (2026-08-04) — Copilot report block (fill and return)

```
### 1.0.24 smoke A — Section A gate (required)
Extension version installed: ______ (must be 1.0.24 — Marketplace only, no VSIX)
Reload Window done: yes / no
Pair run with human: yes / no
Flow package chosen: yes / no
Active env kind (human-designated): local / qa / staging / other (no hostname)
Healthy env entry URL health: app HTML / 404 / NoSuchKey / other: ______
A1 API present + customChecks wrapper used: PASS | FAIL — …
A2 correct labels pass: PASS | FAIL — …
A3 wrong labels fail (not hollow): PASS | FAIL — …
A3b HTML matrix L2 fail (not skip): PASS | FAIL — …
A3c Violations badge opens Flow Runner: PASS | FAIL — …
A4 focus trap Tab+Shift+Tab: PASS | FAIL | SKIP — …
**Section A overall: PASS | FAIL**
**Gate close recommendation: CLOSE | KEEP OPEN** (CLOSE only if Section A overall PASS)
Notes / Output excerpt (neutral — no org/repo/host names):
______

### 1.0.24 smoke B — P1-11 catch-up (optional)
B1 Confluence Connect→Publish: PASS | FAIL | SKIP — …
B2 CLI vendor honesty: PASS | FAIL | SKIP — …
B3 Why on disabled chips: PASS | FAIL | SKIP — …
B4 ENV-FALLBACK URL honesty: PASS | FAIL | SKIP — …
**Section B overall: PASS | FAIL | PARTIAL | SKIPPED**
Notes (neutral): ______
```

### What Copilot says to the human at start of session

> Open this brief (same GitHub/raw link you already use). Install Marketplace **1.0.24** only (no VSIX), Reload Window, confirm version. We do **Section A** first: `keyboardTabJourney` must use `customChecks: […]` inside `checkA11y`. Correct labels pass; wrong labels must fail; L2 in the HTML report must show fail; the violations badge must open Flow Runner. Gates (a)/(b) are already closed — do not make them the main todo. You click; I read Output and fill the report block. We stop if the URL is not app HTML. **Gate closes only when Section A overall is PASS.**

### HISTORICAL — prior floors

Earlier briefs targeted **1.0.11–1.0.23** and Gates **(a)**/**(b)**. Prefer **1.0.24** + **Section A** for all new runs. Prior TODO tables that only mention Gate 3 or 1.0.18/1.0.19/1.0.23 as current are obsolete for this adoption session.

# A11y Studio — Copilot brief (laptop + vendor)

## COPILOT — OPEN THIS URL (CURRENT 2026-08-19b)

**GitHub (read here):** https://github.com/a11ystudio/media/blob/main/docs/enterprise-adoption-laptop.md  

**Raw (fetch / paste):** https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-adoption-laptop.md  

**Cache-bust fetch (prefer if page looks old):** https://cdn.jsdelivr.net/gh/a11ystudio/media@main/docs/enterprise-adoption-laptop.md  

**Do not change this URL.** If the page still says **1.0.24** / **1.0.23** as the *current* floor, or has **no Vendor matrix mapping** section, hard-refresh or use raw / jsDelivr — this file is **1.0.26** + matrix (**2026-08-19b**).

The human cannot paste long chat instructions. This page is the vendor message. **Pick Job A or Job B. Do not mix in one session.**

### WHERE ARE YOU

| You are… | Do **Job** |
| --- | --- |
| Corporate **laptop**, **customer** repo, Marketplace extension only | **A** — Section A + Flow HTML re-smoke. [#303](https://github.com/a11ystudio/a11y-studio/issues/303). **No** vendor-repo coding. |
| Clone of **[a11ystudio/a11y-studio](https://github.com/a11ystudio/a11y-studio)** | **B** — Flow Runner + Playwright **specs** + **POLICY P2**. Unified HTML **report parked**. Do **not** edit `apps/chrome-extension/**`. Do **not** re-do CLI-VENDOR-HTML-ESLINT (Cursor). |

**Human → Copilot (laptop / Job A):**  
> Re-read this GitHub brief (hard-refresh or raw if stale). Install Marketplace **1.0.26** only, Reload Window. Findings **1–6** are **CLOSED since 1.0.24**. Section A: `keyboardTabJourney` via `customChecks`; A2 pass / A3 fail; L2; badge. Also re-smoke **Flow HTML** on 1.0.26. Do **not** use Record Tab for Section A. Wrong origin host → run INVALID.

**Human → Copilot (vendor repo / Job B):**  
> You are in **a11ystudio/a11y-studio**. Read `AI-SNAPSHOT.md` + ledger **NOW**. Unified report / FUNC / CLAR / REPORT = **PARKED**. Chrome Wave-2 = other lane (`apps/chrome-extension/**` off-limits). **CLI-VENDOR-HTML-ESLINT** = Cursor — do **not** re-bundle `studio-cli.cjs`. Implement Flow Runner + spec reliability: **POLICY P2** (filter Problems/scan by `policy.standard` — picker already shipped #323), then Record/Run/spec bugs **only with a failing repro**. `feature/<topic>` from `main`; `pnpm run verify`; PR to `main`.

---

## JOB B — vendor repo (Flow Runner + specs)

Use this only inside **github.com/a11ystudio/a11y-studio**.

| Do | Don’t |
| --- | --- |
| `feature/` from `main`; tests; `pnpm run verify` | Unified HTML report redesign, 0–100 scores, ADA/508/EAA fake filters |
| **POLICY P2** — apply `policy.standard` when listing/gating findings (`wcagLevel` + SC membership; AA includes A) | Invent EN/RGAA engines (P4 HOLD) · **CLI-VENDOR-HTML-ESLINT** (Cursor owns — do not duplicate) |
| Flow Record/Run: storageState cwd, spec codegen, overwrite warn (L5), brittle locators — **with a failing test or Output excerpt** | Touch `apps/chrome-extension/**` |
| Neutral copy — no customer hostnames | Publish VSIX / bump Marketplace unless human said `publish vX.Y.Z` |
| Update your COORDINATOR-BOARD **VS Code / Flow** row at session end | `@codebase` the whole monorepo; recap preflight §1–6 |

Open work SSOT: [vscode-extension-implementation-ledger.md](https://github.com/a11ystudio/a11y-studio/blob/main/docs/specs/vscode-extension-implementation-ledger.md) **NOW**. Live pin: [AI-SNAPSHOT.md](https://github.com/a11ystudio/a11y-studio/blob/main/AI-SNAPSHOT.md).

---

## JOB A — adoption laptop (Marketplace only)

Pair-run protocol. Env keys below are **human-designated for this run only** — not product defaults.

### World product — not one client (read first)

**A11y Studio is a global product.** Named environments (`local`, `qa`, `staging`, `dev2`, …) come from **each repo’s** `a11y-studio.json` → `flowRunner.environments`. The product does **not** prefer any key. Marketplace behavior must stay valid for **any** team worldwide.

**Install Marketplace `a11ystudio.a11y-studio` `1.0.26` only, then Reload Window**, before this smoke. Do **not** keep testing on **≤1.0.25** — skip straight to **1.0.26**.

### Client constraint (non-negotiable)

- **Marketplace only** — Extensions → A11y Studio → **1.0.26**. No VSIX sideload. No vendor-repo files. No build-from-main.
- Never write customer **org**, **repo**, **hostname**, **URL**, or **person** names in chat, Output excerpts, or the report block. Never write **auth-profile** names.
- Use only generic env **kinds** the human confirms (`local` / `qa` / `staging` / `other`), `app HTML` / `404` / `NoSuchKey`, generic path shapes (`tests/a11y/.auth/<profile>.json`).
- Never paste secrets, tokens, or storageState contents.

### Context you must keep straight

| Fact | Meaning for you |
| --- | --- |
| **Floor** | Marketplace **1.0.26** LIVE — Section A + **Flow HTML re-smoke** ([#303](https://github.com/a11ystudio/a11y-studio/issues/303)) |
| **Already CLOSED** | Gate **(a)** known-violation honesty · Gate **(b)** multi-env Run all deny-mismatch (**PASSED** on ≥1.0.21) — **do not** re-prove as the main todo |
| **Your job** | Pair run on the **customer monorepo** laptop only — not the vendor `a11y-studio` repo |
| **wcag-map.json** | **Not required in the customer repo.** Bundled in the Marketplace extension. |
| **Auth profile selected** | Injects Playwright **`storageState`** (saved cookies/session) — it does **not** type username/password into login form steps in a recorded spec |
| **Record flow** | **Not required** for Section A |
| **Tab during Record** | **Does nothing useful** — Playwright codegen does **not** write `keyboard.press('Tab')`. Focus outline during record ≠ keyboard coverage in the spec. Use **Add checkpoint → Keyboard Tab journey (live)** (or paste the Section A `customChecks` pattern). |
| **“Stopped halfway”** | Either (1) unclean stop → partial codegen file, or (2) full spec + brittle locator timeout on **Run**. Not proof that Tab-recording “almost worked.” |
| **Do not claim** | “1.0.26 laptop-validated” or adopt-ready until **Section A overall: PASS** |

---

### Pair testing — who does what

| Role | Does |
| --- | --- |
| **Human** | Clicks panel rows, confirms URL in a browser, inserts/edits journey labels, reads Output with Copilot |
| **Copilot** | Confirms version **1.0.26**, guides GATE PATH, fills the report block, **never** pastes secrets, org, repo, or hostnames |
| **Together** | Finish **Section A** first; optional **Section B** after; stop on red URL |

**Goal (this revision):**

- **Section A (required gate)** — `keyboardTabJourney` via **correct API**; correct labels **pass**; wrong labels **fail** (not hollow); L2 shows fail in HTML matrix; panel opens from violations badge without crash.
- **Section B (optional catch-up)** — P1-11 panel friction checks (Confluence path, CLI vendor honesty, Why on disabled chips, ENV-FALLBACK).

---

### YOUR TODO NOW (2026-08-19) — Marketplace **1.0.26** · Section A + Flow HTML

| # | Todo | Owner | Done when |
| --- | --- | --- | --- |
| **T1** | Confirm extension is **1.0.26** + **Reload Window** | Human + Copilot | Version verified — **not** ≤1.0.25 |
| **T1b** | Copilot re-reads this GitHub brief (same URL) after hard-refresh | Copilot | Brief shows **1.0.26** / Job A vs Job B / **Vendor matrix mapping** — not stale 1.0.24-only |
| **T2** | Flow package chosen; trusted workspace; healthy env URL (human designates) | Human | App HTML (not 404 / `NoSuchKey`) |
| **T3** | **A1** — API present; use **`customChecks: [A11yStudioChecks.keyboardTabJourney([...])]`** inside `checkA11y` options (never as 2nd arg alone) | Human + Copilot | No opaque `replace` crash; clear error if API misused |
| **T4** | **A2** — Run with **correct** focus labels → must **PASS** | Human + Copilot | Journey green; L1 axe may pass; L2 may pass or N/A if no contract |
| **T5** | **A3** — Wrong labels / reversed order → must **FAIL** (hollow green = FAIL); HTML matrix **L2 = fail** | Human + Copilot | Violations in Problems + L2 fail in report |
| **T6** | Click **“N flow violations”** status badge → Flow Runner panel opens (no “Could not open” / reload) | Human + Copilot | Panel opens |
| **T7** | **A4** (if dialog available) — `focusTrapActive` Tab + Shift+Tab | Human + Copilot | PASS or SKIP with reason |
| **T8** | Fill **report block** → [#303](https://github.com/a11ystudio/a11y-studio/issues/303) | Copilot | **Section A overall** decided |
| **T8b** | **Flow HTML re-smoke** on 1.0.26 (open latest HTML; transcript + findings present; not hollow 0-checkpoint pass) | Human + Copilot | Note PASS/FAIL on #303 |
| **T9** | Optional **Section B** only after A | Both | PARTIAL OK |

**Not your todo (Job A):** Re-running Gate (a)/(b) as the *primary* smoke · Expand-all · VSIX · vendor-repo coding · naming customer org/repo/hostname/auth-profile · treating unrelated locator timeouts as Section A FAIL · **npm-install `@html-eslint`** into the customer repo (that is **not** the product fix) · treating **UX1/UX2** as 1.0.26 Blocks until you re-run them on **1.0.26**. **Job B** is vendor-repo coding (separate session).

**Adopt messaging:** **OFF** until human/maintainer promotes after **Section A PASS**.

---

## CURRENT — Vendor matrix mapping (2026-08-19)

Laptop Copilot pasted an internal go/no-go sheet. **Do not copy customer org, repo, hostname, auth-profile names, or package folders into chat, Output excerpts, or [#303](https://github.com/a11ystudio/a11y-studio/issues/303).** Use generic env kinds (`local` / `qa` / `staging`) only.

**Name clash:** **Section A** A1–A4 below = keyboard Tab journey (required gate). **Matrix-A1 / Matrix-A2 / Matrix-B1** = Gate (b) multi-env Run all (confirmatory only). Never mix the IDs in the report block.

| Matrix ID | Vendor mapping | Job A on **1.0.26** |
| --- | --- | --- |
| **C1–C5** | Support bundle: active env, auth profile present, run/skip list, skip reason, pre-exec decisions | **Accept** — already locally Passed. Do not re-open as Block. |
| **R1** | Versioned Marketplace cadence | **Accept** |
| **AI1** | Optional AI stays opt-in / no URL = no egress | **Accept** (config) |
| **REP2** | Zero checkpoints = not-scanned, never a clean pass | **Accept** (historical) — optional re-smoke after auth refresh |
| **Matrix-A1 / A2 / B1** | Gate (b) Run all deny-mismatch | **Confirmatory only** after auth refresh — **not** the primary todo. Closed as product work since **≥1.0.21**. One spot-check; do not re-litigate. |
| **Matrix-A3** | Skipped env: no auth read | **Confirmatory** — regenerate support bundle on 1.0.26; expect `skip` + no auth file read for skipped specs |
| **REP1** | Fresh Flow HTML (checkpoints, findings, tree, L2) | **Required** with Section A / T8b after auth refresh |
| **UX1** | CLI install → panel refresh without Reload Window | **Re-verify on 1.0.26** — shipped **P1-07 / #280**. Quoted “stale until Reload” is **not** a 1.0.26 Block until it fails after Reload on 1.0.26. |
| **UX2** | Monorepo eslint discovery | **Re-verify on 1.0.26** — shipped **P1-08 / #280**. Live copy is `No eslint.config.* in <folder> or any parent folder`. The old `in this folder` string is **pre-#280**. Re-run nested scan; if it still fails, then escalate. |
| **UX3 / PUB1** | Vendored `studio-cli.cjs` runnable (`--help` / `summarize --flow`) | **Vendor bug on 1.0.26** — file present ≠ runnable. `Cannot find module '@html-eslint/eslint-plugin'` is **CLI-VENDOR-HTML-ESLINT** (Cursor). **Do not** npm-install `@html-eslint` into the customer repo as the product path. **Do not** treat as a customer-repo defect. Note FAIL on B2 / PUB1; continue Section A. Fix rides a **later Marketplace cut** + Refresh vendored engine. |
| **PUB2** | Repo-owned Confluence publisher script | **Accept with mitigation** — keep using it until vendor CLI ships the html-eslint bundle |
| **R2** | Formal JSON schema doc | **Not a Marketplace Block** — nice-to-have |
| **MCP1 / MCP2** | MCP npx / live scan | **Not a Marketplace Block** — local IT / npm cache; MCP is not bundled as the Marketplace engine |
| **AI2** | Draft tests via customer worker | **Not a Marketplace Block** — worker stays off until privacy approves |

**Job B (vendor repo only):** POLICY P2 + Flow/spec bugs with a failing repro. **Do not** implement CLI-VENDOR-HTML-ESLINT (Cursor). **Do not** edit `apps/chrome-extension/**`. Unified HTML report remains **parked**.

---

## FINAL EXPECTATION — when is the required gate CLOSED?

**Section A overall = PASS** (and the gate may close) **only if all of the following are true:**

1. Extension details show **1.0.26** (Marketplace, after Reload).
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

1. Extensions → **A11y Studio** → **1.0.26** (Marketplace — **no VSIX**).
2. Command Palette → **Developer: Reload Window**.
3. Confirm version on the Extensions detail page — must say **1.0.26**.

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

**Anti-pattern:** Do **not** spend the session on **Record flow** hoping Tab/outline appears in the spec. Codegen will not emit those steps. Section A proves **`keyboardTabJourney` at run time**, not recorder fidelity.

1. Page with a clear Tab order. Labels must match **live focus announcements** (human reads focus with Tab once in a normal browser; Copilot helps phrase tokens).
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
| B2 | VSIX-vendored Studio CLI | Panel does **not** tell users to install public npm `@a11ystudio/cli`. **Known 1.0.26:** `node .a11y-studio/studio-cli.cjs --help` may throw `@html-eslint/eslint-plugin` — **vendor** (UX3/PUB1). Record FAIL; do not npm-install the plugin. |
| B3 | Disabled Flow/Reports actions | Inline **Why · …** (not hover-only) |
| B4 | Named env with **no** URL | No silent localhost inherit; Run/Record gated with reason |

### Step 5 — Evidence

1. Fill **Copilot report block** below.
2. Prefer also commenting the same templates on vendor issue [#303](https://github.com/a11ystudio/a11y-studio/issues/303) if the human has access — **this media URL stays the Copilot bookmark**.

---

## CURRENT — If FAIL (triage together)

| Output signal | Owner | Next action |
| --- | --- | --- |
| Still on **≤1.0.25** | **install** | Update Marketplace to **1.0.26** + Reload — retest invalid until then |
| Brief still says **1.0.24** as *current* floor (no Job A/B) | **stale cache** | Refetch raw / cache-bust URL above |
| URL / 404 / `NoSuchKey` | **environment** | Stop; env owners fix URL |
| `Cannot read properties of undefined (reading 'replace')` | **install / API** | Must be on **≥1.0.24** + use `customChecks: []` wrapper |
| A3 still **passes** with wrong labels | **product** | Hollow success — escalate (blocker) |
| L2 shows `— skip` but findings exist | **product** | Escalate (keyboard customs → L2 since 1.0.24) |
| Badge → “Could not open Flow Runner” | **product** | Escalate (fixed 1.0.24 — retest on 1.0.26) |
| Spec timeout on login `getByTestId` / username | **spec / app** | Not Section A — fix journey or storageState |
| Checkpoint URL host ≠ env `baseUrl` (e.g. public `www.*` while env is `local.*`) | **session / product** | Treat run **INVALID** — re-save auth, re-run A2/A3; **1.0.26** badges URL-origin mismatch |
| Findings **1–6** listed as open while on **≥1.0.24** | **stale Copilot memory** | Re-read this brief — those are **CLOSED since 1.0.24** |
| Record flow / Tab presses / `test('test')` | **not Section A** | Record≠keyboard; use Add checkpoint journey for A |
| `Cannot find module '@html-eslint/eslint-plugin'` from `.a11y-studio/studio-cli.cjs` | **vendor (1.0.26)** | Known UX3/PUB1. Note it. Do **not** npm-install html-eslint. Continue Section A. |
| Expand all broken | **vendor-roadmap** | Skip |

Do **not** use public sauce-demo as a substitute for this adoption repo.

---

## Document revision

**Document revision:** **2026-08-19b** · **Supersedes all earlier versions of this URL**  
**GitHub:** https://github.com/a11ystudio/media/blob/main/docs/enterprise-adoption-laptop.md  
**Canonical raw:** https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-adoption-laptop.md  

| Field | Value |
| --- | --- |
| **This revision** | **2026-08-19b** — Job A laptop **1.0.26** + matrix mapping · UX3/PUB1 = vendor CLI html-eslint · Job B POLICY P2 (no CLI duplicate) · report parked |
| **Marketplace floor** | **v1.0.26** LIVE |
| **Copilot workspace** | Job A = customer monorepo · Job B = vendor `a11ystudio/a11y-studio` |
| **Naming** | Reports stay **neutral** — no customer org, repo, hostname, or project codenames |
| **URL** | **Unchanged** — same media path Copilot already bookmarks |

### How to read this page (anti-stale)

1. Confirm **Document revision** is **2026-08-19b** (or newer) and floor **v1.0.26**. If brief still says **1.0.24** as *the* current floor with no Job A/B / no **Vendor matrix mapping**, refetch raw URL.
2. Only sections marked **CURRENT** are actionable. **YOUR TODO NOW** + **GATE PATH** + **FINAL EXPECTATION** are the priority.
3. Sections marked **HISTORICAL** are context only.
4. If two bullets disagree, the **newer dated** block wins.

### Install (CURRENT)

**Extension:** Marketplace **`a11ystudio.a11y-studio` `1.0.26`**

1. Extensions → A11y Studio → update to **1.0.26**.
2. **Developer: Reload Window**.
3. Confirm version in Extensions detail.

### Shipped focus for this laptop (1.0.26)

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
| Vendored CLI html-eslint crash (`studio-cli.cjs`) | **Known 1.0.26** — CLI-VENDOR-HTML-ESLINT in next Marketplace cut; laptop: note FAIL, continue Section A |
| L3 visual · Figma · Docker product · adopt media | HOLD until Section A PASS + maintainer promote |

### CURRENT (2026-08-04) — Copilot report block (fill and return)

```
### 1.0.26 smoke A — Section A gate (required)
Extension version installed: ______ (must be 1.0.26 — Marketplace only, no VSIX)
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

### 1.0.26 smoke B — P1-11 catch-up (optional)
B1 Confluence Connect→Publish: PASS | FAIL | SKIP — …
B2 CLI vendor honesty: PASS | FAIL | SKIP — … (1.0.26 html-eslint crash = known vendor UX3; not a customer-repo Block)
B3 Why on disabled chips: PASS | FAIL | SKIP — …
B4 ENV-FALLBACK URL honesty: PASS | FAIL | SKIP — …
**Section B overall: PASS | FAIL | PARTIAL | SKIPPED**
Notes (neutral): ______

### 1.0.26 matrix mapping (fill after Section A; no hostnames / auth-profile names)
C1–C5 / R1 / AI1 / REP2: Accept (do not re-open) — notes: ______
Matrix-A1/A2/B1 Gate (b) confirmatory: PASS | FAIL | SKIP — …
Matrix-A3 support-bundle skip-env no auth read: PASS | FAIL | SKIP — …
REP1 fresh Flow HTML: PASS | FAIL | SKIP — …
UX1 panel refresh after CLI install (1.0.26): PASS | FAIL | SKIP — …
UX2 nested eslint / parent config (1.0.26; not old “in this folder” copy): PASS | FAIL | SKIP — …
UX3/PUB1 vendored CLI --help (html-eslint): FAIL expected on 1.0.26 | PASS if already on a later cut — …
PUB2 repo Confluence script: Accept with mitigation | FAIL — …
R2 / MCP / AI2: not Marketplace Blocks — notes: ______
```

### What Copilot says to the human at start of session

> Open this brief (same GitHub/raw link). **Laptop:** Marketplace **1.0.26**, Section A + Flow HTML + matrix mapping, [#303](https://github.com/a11ystudio/a11y-studio/issues/303). UX3 html-eslint = vendor, not your repo. **Vendor repo:** Job B — POLICY P2; no CLI-VENDOR-HTML-ESLINT; report parked; no Chrome tree. You click on laptop; I read Output. In vendor repo I implement with tests. **Do not mix jobs.**

### HISTORICAL — prior floors

Earlier briefs targeted **1.0.11–1.0.24** and Gates **(a)**/**(b)**. Prefer **1.0.26** + **Section A** (Job A) or **Job B** in the vendor repo. Prior TODO tables that only mention Gate 3 or 1.0.18–1.0.24 as *current* are obsolete.

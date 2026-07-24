# A11y Studio — enterprise adopt-existing laptop brief

## COPILOT — OPEN THIS URL (CURRENT 2026-07-24)

**GitHub (read here):** https://github.com/a11ystudio/media/blob/main/docs/enterprise-adoption-laptop.md  

**Raw (fetch / paste):** https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-adoption-laptop.md  

**Cache-bust fetch (prefer if page looks old):** https://cdn.jsdelivr.net/gh/a11ystudio/media@e14bcc3/docs/enterprise-adoption-laptop.md

The human cannot paste long chat instructions into you. This GitHub page is the vendor's message to you **and** the shared script for **human + Copilot pair testing**.

### World product — not one client (read first)

**A11y Studio is a global product.** Named environments (`local`, `qa`, `staging`, `dev2`, …) come from **each repo’s** `a11y-studio.json` → `flowRunner.environments`. The product does **not** prefer any key. Marketplace behavior must stay valid for **any** team worldwide.

This brief is **pair-run protocol for one adoption laptop session**. Env keys below are **human-designated for this run only** — not product defaults.

**Install Marketplace `a11ystudio.a11y-studio` `1.0.18` only, then Reload Window**, before any Gate retest. Do **not** keep testing on **1.0.17**, **1.0.16**, or earlier — skip straight to **1.0.18**.

### Client constraint (non-negotiable)

- **Marketplace only** — Extensions → A11y Studio → **1.0.18**. No VSIX sideload. No vendor-repo files. No build-from-main.
- Never write customer **org**, **repo**, **hostname**, **URL**, or **person** names in chat, Output excerpts, or the report block.
- Use only generic env **kinds** the human confirms (`local` / `qa` / `staging` / `other`), `app HTML` / `404` / `NoSuchKey`, generic path shapes (`tests/a11y/.auth/<profile>.json`).
- Never paste secrets, tokens, or storageState contents.

### Context you must keep straight

| Fact | Meaning for you |
| --- | --- |
| **Floor** | Marketplace **1.0.18** LIVE — HOT F1–F9 (auth path, TLS ignoreHTTPSErrors, AST checkpoint, env-prefix filter, Verify row, etc.) |
| **Freeze** | **ON** until laptop Gates **(a)** + **(b)** PASS on **1.0.18** (or a new written waive) |
| **Your job** | Pair run on the **customer monorepo** laptop only — not the vendor `a11y-studio` repo |
| **Healthy env (this session)** | Human designates. **For this laptop run:** env key **`qa`**. If human says **`staging`** is dead → do not select it |
| **Also exercise** | Env key **`local`** (or human’s local-flow equivalent) for Gate **(b)** filter proof |
| **Record flow** | **Not required** for these gates |
| **Highest-risk step** | **Auth / `.auth` / `storageState` path** (must resolve under Flow package) |
| **Do not claim** | “Gate 3 DoD” or “catches violations verified” until **(a)** and **(b)** both PASS |

---

### Pair testing — who does what

| Role | Does |
| --- | --- |
| **Human** | Clicks panel rows, Setup auth (headed login / MFA), confirms URL in a browser, reads Output with Copilot |
| **Copilot** | Runs Command Palette commands when allowed, reads Output / `{ ok, gates }` / support bundle, fills the report block, **never** pastes secrets, org, repo, or hostnames |
| **Together** | Walk **GATE PATH** below; stop on red URL; escalate with support bundle |

**Goal (this revision):**

- **Gate (a)** — Known-violation fixture / scan path shows **≥1** finding (not hollow PASS).
- **Gate (b)** — Flow runs with env-prefix filter: **`qa`** (+ auth) and **`local`** (or local-flow) — unrelated env specs skipped; no wrong-env URL storm.

---

### YOUR TODO NOW (2026-07-24) — Marketplace **1.0.18** · Gates (a)+(b)

| # | Todo | Owner | Done when |
| --- | --- | --- | --- |
| **T1** | Confirm extension is **1.0.18** + **Reload Window** | Human + Copilot | Version verified — **not** 1.0.17 |
| **T2** | Check healthy env entry URL (human: **`qa`**) — app HTML vs 404 / `NoSuchKey`. Skip dead envs (here: **`staging`**) | Human (Copilot records) | Q1 answered |
| **T3** | Flow package chosen + active env + auth profile for that env | Human | Panel shows env + auth |
| **T4** | **Diagnose Node & Playwright** → PASS | Human or Copilot | Output excerpt |
| **T5** | **Gate (a)** — known-violation path → **≥1 finding** | Human + Copilot | Count ≥1 recorded |
| **T6** | **Gate (b)** — Run flow / Guided adoption on **`qa`**, then **`local`** (filtered) | Human + Copilot | Filter behavior confirmed |
| **T7** | Write **support bundle** after run or on FAIL | Copilot / Human | Path reported |
| **T8** | **Skip Expand all** — known FAIL; do not block | Both | Noted skipped |
| **T9** | If URL unhealthy → **stop**; report env **kind** only | Both | Stopped cleanly |

**Not your todo:** Expand-all fixes, VSIX install, vendor-repo coding, naming any customer org/repo/hostname in reports.

**Feature freeze:** **ON** after 1.0.18 — no Marketplace bump until Gates (a)+(b) PASS or a new written waive.

---

## CURRENT — Run modes (read once, then ignore)

**Choose run mode…** is three shortcuts. For Gate (b) you typically want **Guided adoption** or **Audit only**.

| Mode | What it runs | Use when |
| --- | --- | --- |
| **Guided adoption (Section B)** | Diagnose → find specs → **Run all flow tests** | Default laptop flow path |
| **Audit only** | Run all flow tests only | Diagnose already green |
| **Audit + Confluence publish** | Run all, then Confluence publish | After flow PASS + publish configured |

| Gate | Meaning |
| --- | --- |
| **1** | Diagnose — Node + Playwright ready |
| **2** | Runnable Flow specs discovered (not only `*.setup.spec.ts`) |
| **3** | **Run all flow tests** succeeded (legacy Section B label) |
| **(a)** | Known-violation → **≥1 finding** ← **required this revision** |
| **(b)** | Env-prefix filter on **`qa`** + **`local`** ← **required this revision** |
| Record | SKIPPED — out of scope |

---

## CURRENT — GATE PATH (do in order)

Copy this checklist into the Copilot chat on the **customer monorepo** laptop. Check off together.

### Step 0 — Install (Marketplace only)
1. Extensions → **A11y Studio** → **1.0.18** (Marketplace — **no VSIX**).
2. Command Palette → **Developer: Reload Window**.
3. Confirm version on the Extensions detail page — must say **1.0.18**.

### Step 1 — Open Flow Runner
1. Activity Bar → **A11y Studio** → **Flow Runner**.
2. **Choose Flow package** = folder that owns `a11y-studio.json` and Flow specs.
3. Confirm panel shows Playwright / Diagnose / Verify rows (plumbing).

### Step 2 — URL health (hard stop if red)
1. Ask the human: **which Flow environment key is healthy?** On **this** laptop session: **`qa`**.
2. Select that environment. **Do not** select keys the human marked dead (here: **`staging`**).
3. Human opens the **same entry URL** in Chrome/Edge.
4. Verdict: **App HTML** → continue. **404** / **NoSuchKey** → **STOP**.
5. Copilot records only: env kind + health — **no hostname**.

### Step 3 — Auth (highest-risk FAIL)
1. Under **Auth**, select or **Add auth profile** for the healthy env (this session: **`qa`**).
2. Human completes **Setup auth** / Save auth state (MFA if needed).
3. Confirm file under Flow package: `tests/a11y/.auth/<profile>.json` (or configured testDir `.auth/`).
4. If Output says `storageState` / `.auth` **ENOENT** → re-run Setup auth; do not invent paths.

### Step 4 — Diagnose
1. Run **Diagnose Node & Playwright**.
2. Output → **A11y Studio** — need **PASS**.

### Step 5 — Gate (a) known-violation (≥1 finding)
1. Human opens / runs the **known-violation** fixture or scan path they use for this adoption.
2. Copilot confirms Output / Problems / report shows **at least one** accessibility finding.
3. **0 findings = FAIL** for Gate (a) — do not call it verified.

### Step 6 — Gate (b) env-prefix filter (`qa` + `local`)
1. Active env = **`qa`** (+ auth). Run **Guided adoption** or **Run all flow tests**.
2. Confirm unrelated env specs are skipped (no wrong-env URL storm).
3. Switch to **`local`** (or human’s local-flow key). Re-run. Confirm filter again.
4. Copilot copies machine result / Output excerpt into the report — **neutral** wording only.
5. **Skip Expand all**.

### Step 7 — Evidence
1. **Write support bundle…** → `.a11y-studio/support-bundle.json` (no secrets).
2. Fill **Copilot report block** below and return it to the vendor chat / human.

---

## CURRENT — If FAIL (triage together)

| Output signal | Owner | Next action |
| --- | --- | --- |
| Still on **1.0.17** or older | **install** | Update Marketplace to **1.0.18** + Reload — retest invalid until then |
| URL / 404 / `NoSuchKey` | **environment** | Stop; env owners fix URL |
| `storageState` / `.auth` ENOENT | **repo / human** | Setup auth again under Flow package |
| Playwright / Node / Chromium / PATH | **laptop** | Diagnose `firstAction` |
| Gate (a) = 0 findings | **product / fixture** | Escalate with support bundle — hollow PASS |
| Wrong-env URL storm | **product** | Escalate — env-prefix filter not applied |
| Expand all broken | **vendor-roadmap** | Skip |

Do **not** use public sauce-demo as a substitute for this adoption repo.

---

## Document revision

**Document revision:** **2026-07-24** · **Supersedes all earlier versions of this URL**  
**GitHub:** https://github.com/a11ystudio/media/blob/main/docs/enterprise-adoption-laptop.md  
**Canonical raw:** https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-adoption-laptop.md  

| Field | Value |
| --- | --- |
| **This revision** | **2026-07-24** — Marketplace **1.0.18**; Gates **(a)** + **(b)**; Marketplace-only client |
| **Marketplace floor** | **v1.0.18** LIVE |
| **Feature freeze** | **ON** until (a)+(b) PASS or new waive |
| **Copilot workspace** | **Customer monorepo only** |
| **Naming** | Reports stay **neutral** — no customer org, repo, hostname, or project codenames |

### How to read this page (anti-stale)

1. Confirm **Document revision** is **2026-07-24** (or newer) and floor **v1.0.18**. If brief still says **1.0.17**, refetch raw URL (hard refresh / cache-bust).
2. Only sections marked **CURRENT** are actionable. **YOUR TODO NOW** + **GATE PATH** are the priority.
3. Sections marked **HISTORICAL** are context only.
4. If two bullets disagree, the **newer dated** block wins.

### Install (CURRENT)

**Extension:** Marketplace **`a11ystudio.a11y-studio` `1.0.18`**

1. Extensions → A11y Studio → update to **1.0.18**.
2. **Developer: Reload Window**.
3. Confirm version in Extensions detail.

### Shipped in 1.0.18 (exercise on this laptop)

| Item | Why it matters |
| --- | --- |
| **storageState flow-package-relative** | Auth path resolves under Flow package (HOT F1) |
| **ignoreHTTPSErrors URL health** | TLS / cert edge cases don’t false-stop health (F2) |
| **AST checkpoint insert** | Known-violation / checkpoint path not hollow (F3) |
| **Env-prefix filter** | `qa` / `local-flow` style basenames skip wrong env (F4) |
| **Verify row / Record auth notice** | Panel clarity (F5–F6) |
| **Support bundle envs + Confluence token alias** | Escalation / publish (F7–F9) |

### Known deferred

| Item | Status |
| --- | --- |
| **Expand all** on Flow Runner | Known FAIL — **skip** (**T8**); vendor later |

### CURRENT (2026-07-24) — Copilot report block (fill and return)

```
Extension version installed: ______ (must be 1.0.18 — Marketplace only, no VSIX)
Reload Window done: yes / no
Pair run with human: yes / no
Flow package chosen: yes / no
Active env kind (human-designated): qa / local / staging / other (no hostname)
Healthy env entry URL health: app HTML / 404 / NoSuchKey / other: ______
Auth profile saved for that env (.auth file present): yes / no / n/a
Diagnose: PASS / FAIL — firstAction if any: ______
Gate (a) known-violation findings count: ______ (≥1 required)
Gate (b) env filter on qa: PASS / FAIL / SKIPPED — notes: ______
Gate (b) env filter on local: PASS / FAIL / SKIPPED — notes: ______
Paste { ok, gates } or Output excerpt (neutral):
______
Support bundle path: ______
Expand all: SKIPPED (known FAIL)
Record flow: SKIPPED (not required)
Notes (neutral — no org/repo/host names): ______
```

### What Copilot says to the human at start of session

> Open this brief (GitHub or raw link). Install Marketplace **1.0.18** only (no VSIX), Reload Window. For **this** pair run the healthy env is **`qa`** (skip **`staging`** if dead). We need Gate **(a)** ≥1 finding and Gate **(b)** env filter on **`qa`** + **`local`**. You click auth and confirm the URL; I read Output and fill the report block. We stop if the URL is not app HTML. We skip Expand all.

### HISTORICAL — prior floors

Earlier briefs targeted **1.0.11–1.0.17**. Prefer **1.0.18** for all new runs. Prior TODO tables that only mention Gate 3 without Gates **(a)**/**(b)** are obsolete for this adoption session.

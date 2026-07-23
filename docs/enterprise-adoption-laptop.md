# A11y Studio — enterprise adopt-existing laptop brief

## COPILOT — OPEN THIS URL (CURRENT 2026-07-23T22:40Z)

**GitHub (read here):** https://github.com/a11ystudio/media/blob/main/docs/enterprise-adoption-laptop.md  

**Raw (fetch / paste):** https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-adoption-laptop.md  

**Cache-bust fetch (prefer if page looks old):** https://cdn.jsdelivr.net/gh/a11ystudio/media@PIN_AFTER_PUSH/docs/enterprise-adoption-laptop.md  

The human cannot paste long chat instructions into you. This GitHub page is the vendor's message to you **and** the shared script for **human + Copilot pair testing**.

**Install Marketplace `a11ystudio.a11y-studio` `1.0.17` (or newer), then Reload Window**, before any Section B / Gate 3 retest. Do **not** keep testing on **1.0.16**, **1.0.15**, or earlier — skip straight to **1.0.17**.

### Security (non-negotiable)

- Never write customer **org**, **repo**, **hostname**, **URL**, or **person** names in chat, Output excerpts, or the report block.
- Use only: `local` / `qa` / `staging` / `other`, `app HTML` / `404` / `NoSuchKey`, generic path shapes (`tests/a11y/.auth/<profile>.json`).
- Never paste secrets, tokens, or storageState contents.

### Context you must keep straight

| Fact | Meaning for you |
| --- | --- |
| **Floor** | Marketplace **1.0.17** LIVE — includes **1.0.16** Gate 3 hotfixes **plus** panel Diagnostics / Run picker / silent Expand / status-bar |
| **Freeze** | **ON** after **1.0.17** — next bump only after Gate 3 PASS or a new written waive |
| **Your job** | Gate 3 pair run on the **customer monorepo** laptop only — not the vendor `a11y-studio` repo |
| **Agreed healthy env** | **`qa`** — use this for Gate 3. **`staging` is the known-dead target** (404 / `NoSuchKey`) on this laptop — do **not** select it for Gate 3 |
| **Record flow** | **Not required** for Gate 3 — automation runs **existing** specs. Recording-exit fixes are for Record paths; they cannot sink Gate 3 |
| **Highest-risk step** | **Step 3 — Auth / `.auth` / `storageState` path** |
| **What is new vs 1.0.15** | Recording exit · storageState · env-scoped Gate 3 · Diagnostics section · Run-all Quick Pick · quieter Expand · status-bar colors · Install Studio CLI CTA |
| **P0-1 / P0-2** | Fixed since **1.0.16** (shipped again in **1.0.17**) — retest on **1.0.17**; never stay on 1.0.15 |
| **1.0.17 publish** | **Written waive** (Copilot was stuck on 1.0.15). Legitimate. **Gate 3 still open**; freeze stays **ON** |

---

### Pair testing — who does what

| Role | Does |
| --- | --- |
| **Human** | Clicks panel rows, Setup auth (headed login / MFA), confirms URL in a browser, reads Output with Copilot |
| **Copilot** | Runs Command Palette commands when allowed, reads Output / `{ ok, gates }` / support bundle, fills the report block, **never** pastes secrets, org, repo, or hostnames |
| **Together** | Walk **GATE 3 PATH** below step-by-step; stop on red URL; escalate with support bundle |

**Goal:** Gate 3 **PASS** = **Run all flow tests** succeeds on the agreed healthy **`qa`** environment with matching auth. Expand all is **out of scope**. **Do not** use **`staging`** for this run — it is the known-dead URL on this laptop.

---

### YOUR TODO NOW (2026-07-23) — Gate 3 pair run on **QA**

| # | Todo | Owner | Done when |
| --- | --- | --- | --- |
| **T1** | Confirm extension is **1.0.17** + **Reload Window** | Human + Copilot | Version verified |
| **T2** | Check **`qa`** entry URL health (app HTML vs 404 / `NoSuchKey`) in a normal browser — **not** `staging` | Human (Copilot records) | Q1 answered |
| **T3** | Flow package chosen + active env = **`qa`** + auth profile saved for **`qa`** | Human | Panel shows env + auth |
| **T4** | **Diagnose Node & Playwright** → PASS (Gate 1) | Human or Copilot | Output excerpt |
| **T5** | If URL = **app HTML** → run **Guided adoption (Section B)** or Command Palette **Run adoption Section B gates** | Human + Copilot | Paste `{ ok, gates }` |
| **T6** | Write **support bundle** after Section B or on FAIL | Copilot / Human | Path reported |
| **T7** | **Skip Expand all** — known FAIL; do not block Gate 3 | Both | Noted skipped |
| **T8** | If URL unhealthy → **stop**; report env only (no selector patches) | Both | Stopped cleanly |
| **T9** | Optional: Integrations → Confluence **Set token** row visible (do not paste token) | Human | yes / no |

**Not your todo:** Expand-all fixes, world-class wizard, sidebar redesign, Chrome/Figma, sauce-demo as Gate 3 substitute, vendor-repo coding, naming any customer org/repo/hostname in reports (use **example** / generic labels only).

**Feature freeze:** **ON** after 1.0.17 — no Marketplace bump until Gate 3 PASS or a new written waive.

---

## CURRENT — Run modes (read once, then ignore)

**Choose run mode…** is three shortcuts. For Gate 3 you want **Guided adoption**.

| Mode | What it runs | Use when |
| --- | --- | --- |
| **Guided adoption (Section B)** | Diagnose → find specs → **Run all flow tests** | **Default for Gate 3 / laptop DoD** |
| **Audit only** | Run all flow tests only | Gates 1–2 already green |
| **Audit + Confluence publish** | Run all, then Confluence publish | After Gate 3 PASS + publish configured |

**Section B** is not a separate panel tab — it is the Guided adoption automation (Gates 1–3). **Record flow is NOT required for Gate 3** — Gate 3 runs **existing** Flow specs. Recording process-exit cannot sink this gate; be most careful on **Step 3 (auth)**.

| Gate | Meaning |
| --- | --- |
| **1** | Diagnose — Node + Playwright ready |
| **2** | Runnable Flow specs discovered (not only `*.setup.spec.ts`) |
| **3** | **Run all flow tests** succeeded ← **pass this** |
| Record | SKIPPED in automation — needs interactive browser; **out of scope for Gate 3** |

---

## CURRENT — GATE 3 PATH (do in order)

Copy this checklist into the Copilot chat on the **customer monorepo** laptop. Check off together.

### Step 0 — Install
1. Extensions → **A11y Studio** → **1.0.17**.
2. Command Palette → **Developer: Reload Window**.
3. Confirm version on the Extensions detail page.

### Step 1 — Open Flow Runner
1. Activity Bar → **A11y Studio** → **Flow Runner**.
2. **Choose Flow package** = folder that owns `a11y-studio.json` and Flow specs (often a dedicated a11y / Playwright package — **not** a random UI package).
3. Confirm panel shows Playwright / Diagnose rows (plumbing).

### Step 2 — URL health (hard stop if red)
1. Select the **`qa`** environment — the **agreed healthy** remote for this Gate 3 run.
2. **Do not** select **`staging`** for Gate 3 on this laptop — it is the **known-dead** target (404 / `NoSuchKey`). Picking it triggers the hard stop and wastes the session.
3. Human opens the **same `qa` entry URL** in Chrome/Edge.
4. Verdict:
   - **App HTML** (login or app shell) → continue.
   - **404** / **NoSuchKey** / empty error page → **STOP**. Fill report: URL unhealthy. Env owners fix. Do **not** chase selectors.
5. Copilot records only: `app HTML` / `404` / `NoSuchKey` / `other` — **no hostname**. Env kind must be **`qa`**.

### Step 3 — Auth (highest-risk Gate 3 FAIL — watch carefully)
1. Under **Auth**, select or **Add auth profile** for **`qa`** (not staging).
2. Human completes **Setup auth** / Save auth state in the headed browser (MFA/OTP if needed).
3. Confirm a file exists under the Flow package: `tests/a11y/.auth/<profile>.json` (or the package’s configured testDir `.auth/`).
4. If Output later says `storageState` / `.auth` **ENOENT** → re-run Setup auth; do not invent paths. Specs must point at the file that exists.

### Step 4 — Gate 1 (Diagnose)
1. Run **Diagnose Node & Playwright** (panel or Command Palette).
2. Open **Output** → channel **A11y Studio** (Flow Runner).
3. Need **PASS**. If FAIL, follow `firstAction` (Install Playwright, Use system Chrome, Fix Apple Silicon Node, open via `code .` from a good shell). Re-run Diagnose until PASS.

### Step 5 — Gate 2 + Gate 3 (Section B)
**Preferred (pair):**
1. Flow Runner → **Choose run mode…** → **Guided adoption (Section B)**.

**Or Command Palette:**
1. **A11y Studio: Run adoption Section B gates**.

2. Watch Output for:
   - `Gate 1 (Diagnose): PASS`
   - `Gate 2 (spec discovery): PASS`
   - `Gate 3 (Run all flow tests): PASS` or **FAIL** + `firstAction`
3. Copilot copies machine result `{ ok, gates }` (and optional `.a11y-studio/section-b-result.json`) into the report block — **neutral** wording only.
4. **Skip Expand all** even if Section B triggers expand — known FAIL; ignore for DoD.

### Step 6 — Evidence
1. **Write support bundle…** (panel plumbing or Command Palette) → `.a11y-studio/support-bundle.json` (no secrets).
2. Fill **Copilot report block** below and return it to the vendor chat / human.

---

## CURRENT — If Gate 3 FAIL (triage together)

| Output signal | Owner | Next action |
| --- | --- | --- |
| URL / 404 / `NoSuchKey` / fail-fast URL | **environment** | Stop coding; env owners fix URL |
| `storageState` / `.auth` ENOENT | **repo / human** | Setup auth again; confirm path under Flow package |
| Playwright / Node / Chromium / PATH | **laptop** | Diagnose `firstAction` (Install / system Chrome / Node) |
| Selector timeout **after** URL+auth OK | **repo** | Escalate with support bundle — do not random-patch on first FAIL |
| Expand all broken | **vendor-roadmap** | Skip; not Gate 3 |

Do **not** use public sauce-demo as a Gate 3 substitute for this adoption repo.

---

## Document revision

**Document revision:** **2026-07-23T22:40Z** · **Supersedes all earlier versions of this URL**  
**GitHub:** https://github.com/a11ystudio/media/blob/main/docs/enterprise-adoption-laptop.md  
**Canonical raw:** https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-adoption-laptop.md  
**Cache-bust (pinned commit):** https://cdn.jsdelivr.net/gh/a11ystudio/media@PIN_AFTER_PUSH/docs/enterprise-adoption-laptop.md  

| Field | Value |
| --- | --- |
| **This revision** | **2026-07-23T22:40Z** — floor **v1.0.17**; Gate 3 on **`qa`** (not dead **`staging`**); Record not required; auth = highest risk |
| **Marketplace floor** | **v1.0.17** LIVE (this-release-only waive for Gate 3 laptop floor) |
| **Feature freeze** | **ON** after 1.0.17 — Gate 3 PASS or new waive before next publish |
| **Copilot workspace** | **Customer monorepo only** — never the `a11y-studio` vendor repo |
| **Naming** | Reports must stay **neutral** — no customer org, repo, hostname, or project codenames |

### How to read this page (anti-stale)

1. Confirm **Document revision** is **2026-07-23T22:40Z** (or newer) and floor **v1.0.17**. If you see **staging** as the Gate 3 target, or floor **v1.0.16** / **v1.0.15**, refetch the **raw** GitHub URL (or a fresh jsDelivr pin).
2. Only sections marked **CURRENT** are actionable. **YOUR TODO NOW** + **GATE 3 PATH** are the priority.
3. Sections marked **HISTORICAL** are context only.
4. If two bullets disagree, the **newer dated** block wins.

### Install (CURRENT)

**Extension:** Marketplace **`a11ystudio.a11y-studio` `1.0.17`**

1. Extensions → A11y Studio → update to **1.0.17**.
2. **Developer: Reload Window**.
3. Confirm version in Extensions detail.

### Shipped in 1.0.17 (exercise on this laptop — includes 1.0.16)

| Item | Why it matters |
| --- | --- |
| **Record terminal exits** | Close browser after Record — status clears; spec no longer rewrites |
| **storageState spawn/config-relative** | Auth path works for workspace config and flow-package cwd |
| **Env-scoped Gate 3** | Active env name in spec basename — skips unrelated env URLs |
| **Includes 1.0.15** | PII file-only resolve · Force stop · Diagnose self-heal · scan storm skip |
| **Support bundle** | Escalation without secrets (**T6**) |
| **URL fail-fast** | Bad URL classified before selector noise — do not pick known-dead **`staging`** |

### Known deferred

| Item | Status |
| --- | --- |
| **Expand all** on Flow Runner | Known FAIL — **skip** (**T7**); vendor later |

### CURRENT (2026-07-23) — Copilot report block (fill and return)

```
Extension version installed: ______ (must be 1.0.17+)
Reload Window done: yes / no
Pair run with human: yes / no
Flow package chosen: yes / no
Active env kind: qa (required for this Gate 3) / local / staging / other (no hostname)
QA entry URL health: app HTML / 404 / NoSuchKey / other: ______
Auth profile saved for qa (.auth file present): yes / no / n/a (public flows)
Diagnose (Gate 1): PASS / FAIL — firstAction if any: ______
Section B / Guided adoption: skipped (URL) / ran
Gate 2 (specs): PASS / FAIL / SKIPPED
Gate 3 (Run all): PASS / FAIL / SKIPPED — firstAction if FAIL: ______
Paste { ok, gates } (or Output excerpt, neutral):
______
Support bundle path: ______
Expand all: SKIPPED (known FAIL)
Record flow: SKIPPED (not required for Gate 3)
Confluence Set token row visible: yes / no
Notes (neutral — no org/repo/host names): ______
```

### What Copilot says to the human at start of session

> Open this brief (GitHub or cache-bust link). We will walk **GATE 3 PATH** Steps 0–6 on **`qa`** together — **not** `staging` (known dead). You click auth and confirm the **qa** URL in a browser; I read Output and fill the report block. Record is not required. We stop if the URL is not app HTML. We skip Expand all.

### HISTORICAL — prior floors

Earlier briefs targeted **1.0.11–1.0.15**. Prefer **1.0.17** for all new runs (skip 1.0.15/1.0.16). Prior TODO tables without the Gate 3 PATH are obsolete.

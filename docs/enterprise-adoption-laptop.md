# A11y Studio — enterprise adopt-existing laptop brief

**Extension:** Marketplace **v1.0.7** LIVE · adopt-existing **`storageState`** repair, **Playwright hoisting**. **Expand all** deferred to **v1.0.8** (known issue — **Collapse all** works; use **Command Palette** when collapsed). **Scan UX** simplify (**Scan all workspace** + per-package rows) targets **v1.0.8** — not required for adoption gates on **1.0.7**.

**Build on this laptop:** **Marketplace latest only** — install or auto-update from **Extensions → A11y Studio**. **Not** a maintainer VSIX, **not** Extension Development Host (F5), **not** a pre-release build. If version ≠ latest Marketplace, update and **Reload Window** before Section B.

Copilot works on the **customer monorepo only** — not the `a11y-studio` vendor repo.

**Layout:** Flow package **`a11y-playwright/`** (or the path in `flowRunner.testDir` inside `a11y-studio.json`). The **workspace** owns **`playwright.config.ts`** and **`yarn a11y`** at the repo root.

---

## Copilot role (read first)

| Do | Do not |
| --- | --- |
| Run **Section A** then **Section B** below on **Marketplace latest** (currently **1.0.7**) | Install from VSIX or assume a dev/F5 build counts as adoption proof |
| Fix **repo-owned** Playwright/spec/config issues (Section A) | Create **`turbo-flow`**, duplicate Playwright packages, or forced **`tests/a11y`** relocations |
| Report **PASS/FAIL** per gate with screenshots + Diagnose log | Treat any long “implementation request” markdown as a **build order** |
| Map stakeholder questions to **Vendor disposition** below | Multi-agent or “implement the whole doc” passes |

---

## World-class implementation request doc

If this repo contains **`A11Y_STUDIO_EXTENSION_WORLD_CLASS_IMPLEMENTATION_REQUEST_*.md`** (often under **`a11y-playwright/`**):

- It is **enterprise requirements input / market signal** — a catalog of desired capabilities.
- It is **not** a Copilot execution spec. **Do not** implement it wholesale.
- **Adoption gate** for the vendor is **Section A + Section B below** on **v1.0.7**, not “complete every §4–§16 item.”

### Vendor disposition (2026-07-10) — §14-style summary

Use this when stakeholders ask “is X supported?”

| Capability | Status | Notes |
| --- | --- | --- |
| **Adopt-existing Flow Runner** (workspace `playwright.config`, package `testDir`, `yarn a11y`) | **Supported now** | v1.0.4–v1.0.7 train; **Diagnose** + repair on reload |
| **Runtime authority / launch layer** (§4.2) | **Supported now** (partial UX) | Login-shell PATH, hoisted Playwright, dual-runtime repair; **Diagnose** shows paths — no full “pick authority” wizard before every run |
| **`storageState` path repair** | **Supported now** | **v1.0.7** — **Diagnose** + **Run all flow tests** rewrite paths before spawn |
| **Auth profiles + setup auth** (§4.6) | **Supported now** | Named profiles, `.auth/*.json`, setup capture; SSO/MFA = manual pause in browser |
| **Run all flow tests + Record flow + HTML/JSON reports** | **Supported now** | Flow Runner panel + Command Palette |
| **Report `kind` conformance/advisory** (§4.8) | **Supported now** | v0.9.16+ in Flow HTML/JSON + CLI rollups |
| **CI generator** (§4.7) | **Supported now** | **`A11y Studio: Generate CI/CD`** — GitHub, GitLab, CircleCI, Jenkins, Azure, CodeBuild |
| **Confluence publish** (§4.5) | **Supported now** (CLI-first) | **`a11ystudio publish --confluence`** + **CLI scan** view when `publish.confluence` configured — **executive-v2** layout; not a full in-extension OAuth wizard |
| **Redaction / PII** (§4.9) | **Supported now** (partial) | `flowRunner.reportRedaction`, default `screenshotsOnViolation: false`; no full “strict/standard/custom” profile UI |
| **Diagnostics / Diagnose** (§4.10) | **Supported now** (partial) | **Diagnose Node & Playwright** + structured `{ ok, reason }` on many Flow commands — not every panel action |
| **Route / coverage discovery** (§4.3) | **Planned** | **`discoverRoutes`** + CLI inventory spec — no full “discovery map” panel |
| **Setup Modes wizard** greenfield / adopt / hybrid (§4.1) | **Planned** | Panel rows + docs today — no unified wizard |
| **Run Mode Selector** Guided / Audit / Audit+Publish (§4.4) | **Planned** | Separate commands today — **best candidate** for next product slice |
| **Preflight / post-run / why-failed panels** (§9) | **Planned** | Partial hints in Diagnose + toasts — no dedicated panels |
| **Config precedence UI** (§10) | **Planned** | `a11y-studio.json` wins; Diagnose surfaces deprecated workspace keys |
| **Scenario matrix §6 in-product** | **Planned** | Laptop brief + maintainer smoke docs — not an extension “scenario runner” |
| **Telemetry §12** | **Not planned v1.x** | No product telemetry |
| **Cross-repo template packs §13** | **Later** | Phase 3 platform |

**Doc corrections (common overstatements):**

- Client doc may say **“no native Confluence publish”** — **incorrect**: Confluence publish ships via **CLI** + extension **CLI scan** when configured.
- Client doc may say **“missing CI bootstrap”** — **incorrect**: **Generate CI/CD** ships for **six** providers.

**Explicit §16 answer (extension-only lifecycle):** **Partial today.** Consultants can author/run flows and publish **via extension + CLI** on adopt-existing layouts. **Guided Journey** headed timeline + **single Run mode picker** are **not** v1.0.7 — track as **planned (§4.4)**.

### Map client §8 gates → this brief

| Client gate | This brief |
| --- | --- |
| **8.1 Setup & discovery** | **Section A** + **Section B gate 2** |
| **8.2 Runtime** | **Section B gate 1** (Diagnose) |
| **8.3 Auth** | **Section A §4** + **Section B gate 3** |
| **8.4 Run modes** | **Not v1.0.7** — report **GAP**, not adoption blocker |
| **8.5 CI** | Validate **Generate CI/CD** separately after Section B |
| **8.6 Security / redaction** | Note **partial** — defaults safe; full policy UI planned |

---

## Before you start

1. **Extensions → A11y Studio** — must be **Marketplace latest** (`a11ystudio.a11y-studio`). Confirm **Help → About** matches the current release (**1.0.7** as of July 2026). **Do not** use **Install from VSIX…** unless the maintainer explicitly sent a retest VSIX.
2. **Reload Window** after install or update.
3. Disable **`ms-playwright.playwright`** if enabled (conflicts with Flow Runner discovery) → **Reload Window** again.
4. Open **Activity Bar → A11y Studio → Flow Runner** and run **Diagnose Node & Playwright** once. Save **Output → A11y Studio Flow Runner**.

---

## Section A — Repo (do first)

Repo-owned **`yarn a11y*`** is the system of record until Section B passes.

1. **`yarn a11y --list`** — must list ≥1 test. If it fails, fix **duplicate `test()` titles** and re-run.
2. **`auth.setup.spec.ts`** — use **`import`**, not **`require`**, when root `package.json` has `"type": "module"`.
3. **`--project`** — names must match workspace **`playwright.config.ts`** projects (`client`, `associate`, `shared`, etc.).
4. **`storageState`** — paths relative to **Playwright config directory** (workspace root in adopt-existing layouts). Auth under **`a11y-playwright/.auth/`** must appear in specs as **`a11y-playwright/.auth/<profile>.json`**, not bare **`.auth/`**. **v1.0.7+:** **Diagnose** and **Run all flow tests** auto-rewrite when auth files exist under the Flow package.

**Do not:**

- Create **`turbo-flow`**, extra **`tests/a11y`** folders, or duplicate Playwright packages unless the team explicitly owns that layout.
- Edit **`.vscode/settings.json`** `nodePath` / `playwrightPath` unless **Diagnose** tells you to.
- Patch Marketplace with a VSIX unless the maintainer sent one for retest (**this laptop run = Marketplace latest only**).

---

## Section B — Extension (four gates)

Use the **Flow Runner** panel and **Command Palette** (`A11y Studio: …`).

**v1.0.7 evaluation:** **Gate 3** (`storageState` / no `.auth/` ENOENT) is the **main fix** in this release. **Expand all** — known limitation (note only, not a ship blocker).

| Gate | Pass criteria |
| --- | --- |
| **1. Diagnose** | Clean preflight; **`yarn a11y --list`** OK in Output; adopt-existing repair lines (config, shims, **`storageState` rewrite** on **1.0.7+**) |
| **2. Spec discovery** | Flow Runner lists specs at the correct path; **`auth.setup.spec.ts`** setup-only (not offered as flow recording); Settings and Flow Runner agree on config path and spec count |
| **3. Run all flow tests** | **Run all flow tests (N specs)** reaches Playwright spawn — not “install Playwright” when `yarn a11y --list` works; not ENOENT on `.auth/` (**1.0.7+** repairs paths before spawn) |
| **4. Record flow** | **Record flow** available when dev server URL is reachable (greyed = start dev server / VPN, not an extension bug) |

**Workspace scan (static lint):** **Activity Bar → Workspace scan → IDE static scan**

| Action | When to use |
| --- | --- |
| **Scan all open packages** / **Scan all workspace** | Full monorepo (label may vary by version) |
| **Scan package: {folder}** | One app — click the package row |
| **Scan active file** | Current editor tab |

Open the **repo root** (folder with `pnpm-workspace.yaml` or npm `workspaces`), not a single sub-app. Custom layouts: `scan.packageRoots` in `a11y-studio.json`.

Results: **Problems** (filter A11y Studio) and **Findings (IDE scan)**.

**Safety:** Do not use **Remove A11y Studio setup** unless intentionally resetting.

---

## Report back (redact secrets)

Paste to the maintainer (text is enough — screenshots optional):

1. Extension version (**Help → About**)
2. **`yarn a11y --list`** output
3. **`flowRunner`** block from **`a11y-studio.json`** (redact URLs if needed)
4. Full **Diagnose** log (**Output → A11y Studio Flow Runner**)
5. **Run all flow tests (N specs)** — pass/fail + first error line
6. **Expand all** — note **known issue 1.0.7**; **Collapse all** PASS/FAIL
7. If world-class doc exists: one line — **“requirements catalog; Section B ___/4”**
8. Verdict: **Section A** PASS/FAIL · **Section B** ___/4 · **Overall** PASS / PARTIAL / BLOCKED

Optional screenshots: Flow Runner panel (spec list + Playwright status), Diagnose Output, one failed run.

---

## Who fixes what

| Issue | Owner |
| --- | --- |
| Duplicate test titles, ESM setup spec, wrong `--project`, wrong `storageState` (pre-1.0.7) | Customer repo |
| Diagnose, panel tree, spec discovery, Playwright resolution, `storageState` auto-repair | A11y Studio vendor |
| Dev server down, VPN, greyed Record/Run | Environment / infra |
| Run Mode Selector, setup wizard, §9 panels | Vendor roadmap — not Copilot on this repo |

---

* [a11ystudio.io](https://a11ystudio.io) · Marketplace `a11ystudio.a11y-studio` · Vendor triage (maintainers): [world-class-request-triage.md](https://github.com/a11ystudio/a11y-studio/blob/main/docs/specs/world-class-request-triage.md)*

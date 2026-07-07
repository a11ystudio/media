# A11y Studio — enterprise adopt-existing laptop brief

**Extension:** Marketplace **v1.0.7** LIVE · adopt-existing **`storageState`** repair, **scan package** UX, **Playwright hoisting**. **Expand all** deferred to **v1.0.8** (known issue — **Collapse all** works; use **Command Palette** when the panel is collapsed).  

Copilot works on the **customer monorepo only** — not the `a11y-studio` vendor repo.

**Layout:** Flow package **`a11y-playwright/`** (or the path in `flowRunner.testDir` inside `a11y-studio.json`). The **workspace** owns **`playwright.config.ts`** and **`yarn a11y`** at the repo root.

---

## Before you start

1. **Extensions → A11y Studio** — confirm version (`a11ystudio.a11y-studio`). **1.0.7** = current Marketplace release (July 2026).
2. **Reload Window** after install or update.
3. For this workspace, disable **`ms-playwright.playwright`** if it is enabled (conflicts with Flow Runner discovery) → **Reload Window** again.
4. Open **Activity Bar → A11y Studio → Flow Runner** and run **Diagnose Node & Playwright** once. Paste the full log from **Output → A11y Studio Flow Runner**.

---

## Section A — Repo (do first)

Repo-owned **`yarn a11y*`** is the system of record until Section B passes.

1. **`yarn a11y --list`** — must list ≥1 test. If it fails, fix **duplicate `test()` titles** and re-run.
2. **`auth.setup.spec.ts`** — use **`import`**, not **`require`**, when root `package.json` has `"type": "module"`.
3. **`--project`** — names must match workspace **`playwright.config.ts`** projects (`client`, `associate`, `shared`, etc.).
4. **`storageState`** — paths are relative to the **Playwright config directory** (workspace root in adopt-existing layouts). Auth under **`a11y-playwright/.auth/`** must appear in specs as **`a11y-playwright/.auth/<profile>.json`**, not bare **`.auth/`**. **v1.0.7+:** **Diagnose** and **Run all flow tests** auto-rewrite existing specs when auth files exist under the Flow package.

**Do not:**

- Create **`turbo-flow`**, extra **`tests/a11y`** folders, or duplicate Playwright packages unless the team explicitly owns that layout.
- Edit **`.vscode/settings.json`** `nodePath` / `playwrightPath` unless **Diagnose** output tells you to.
- Patch Marketplace with a VSIX unless the maintainer sent one for a retest.

---

## Section B — Extension (four gates)

Use the **Flow Runner** panel and **Command Palette** (`A11y Studio: …`).

**v1.0.7 evaluation (Copilot on customer monorepo):** **Run all flow tests** — **storageState** auto-repair on Diagnose/Run; **Playwright hoisting** when workspace owns runtime. **Panel Expand all** — known limitation (report PASS/FAIL; not a ship blocker). **Workspace scan** — use **Scan package:** for 2–3 apps; **Choose package…** for larger monorepos.

| Gate | Pass criteria |
| --- | --- |
| **1. Diagnose** | Clean preflight; **`yarn a11y --list`** OK in Output; adopt-existing repair lines (config, shims, **`storageState` rewrite** on **1.0.7+**) |
| **2. Spec discovery** | Flow Runner lists specs at the correct path; **`auth.setup.spec.ts`** is setup-only (not offered as a flow recording); Settings and Flow Runner agree on config path and spec count |
| **3. Run all flow tests** | **Run all flow tests (N specs)** reaches Playwright spawn — not “install Playwright” when `yarn a11y --list` works; not ENOENT on `.auth/` (**1.0.7+** repairs paths before spawn) |
| **4. Record flow** | **Record flow** is available when the dev server URL is reachable (greyed = start dev server / VPN, not an extension bug) |

**Workspace scan (static lint):** **Activity Bar → Workspace scan → IDE static scan**

| Action | When to use |
| --- | --- |
| **Scan all open packages** | Full monorepo / every discovered package (respects **Switch lint focus** if set) |
| **Scan package: {folder}** | **Best for 2–3 packages** — one click per app; results under **Findings** grouped by folder |
| **Choose package to scan…** | Larger monorepos (many packages) or title-bar picker — opens a list, then scans **one** package |
| **Scan active file** | Current editor tab only |

Open the **repo root** (folder with `pnpm-workspace.yaml` or npm `workspaces`), not a single sub-app, so all packages appear. Custom layouts: `scan.packageRoots` in `a11y-studio.json`.

Results: **Problems** (filter A11y Studio) and **Findings (IDE scan)**.

**Safety:** Do not use **Remove A11y Studio setup** unless intentionally resetting. Cancel any destructive prompt you did not mean to open.

---

## Report back (redact secrets)

Paste to the maintainer via Teams/Slack:

1. Extension version from **Help → About**
2. Output of **`yarn a11y --list`**
3. **`flowRunner`** block from **`a11y-studio.json`** (redact URLs if needed)
4. Full **Diagnose** output (**Output → A11y Studio Flow Runner**)
5. **Run all flow tests (N specs)** — pass/fail and first error line (not **Run this flow test** unless you are debugging one spec)
6. Panel: **Expand all** — note **known issue in 1.0.7** (deferred v1.0.8); **Collapse all** PASS/FAIL
7. Verdict: **Section A** PASS/FAIL · **Section B** ___/4 · **Overall** PASS / PARTIAL / BLOCKED

Optional screenshots: Flow Runner panel (spec list + Playwright status), one failed run if any.

---

## Who fixes what

| Issue | Owner |
| --- | --- |
| Duplicate test titles, ESM setup spec, wrong `--project`, wrong `storageState` (pre-1.0.7) | Customer repo |
| Diagnose, panel tree, spec discovery, Playwright resolution, `storageState` auto-repair | A11y Studio vendor |
| Dev server down, VPN, greyed Record/Run | Environment / infra |

---

* [a11ystudio.io](https://a11ystudio.io) · Marketplace `a11ystudio.a11y-studio`*

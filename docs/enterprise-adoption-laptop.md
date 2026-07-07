# A11y Studio — enterprise adopt-existing laptop brief

**Extension:** Marketplace **v1.0.6** · **2026-07-07**

Copilot works on the **customer monorepo only** — not the `a11y-studio` vendor repo.

**Layout:** Flow package **`a11y-playwright/`** (or the path in `flowRunner.testDir` inside `a11y-studio.json`). The **workspace** owns **`playwright.config.ts`** and **`yarn a11y`** at the repo root.

---

## Before you start

1. **Extensions → A11y Studio** — confirm **1.0.6** (`a11ystudio.a11y-studio`).
2. **Reload Window** after install or update.
3. For this workspace, disable **`ms-playwright.playwright`** if it is enabled (conflicts with Flow Runner discovery) → **Reload Window** again.
4. Open **Activity Bar → A11y Studio → Flow Runner** and run **Diagnose Node & Playwright** once. Paste the full log from **Output → A11y Studio Flow Runner**.

---

## Section A — Repo (do first)

Repo-owned **`yarn a11y*`** is the system of record until Section B passes.

1. **`yarn a11y --list`** — must list ≥1 test. If it fails, fix **duplicate `test()` titles** and re-run.
2. **`auth.setup.spec.ts`** — use **`import`**, not **`require`**, when root `package.json` has `"type": "module"`.
3. **`--project`** — names must match workspace **`playwright.config.ts`** projects (`client`, `associate`, `shared`, etc.).
4. **`storageState`** — paths must match where auth files live. If auth is under **`a11y-playwright/.auth/`**, specs must use **`a11y-playwright/.auth/<profile>.json`** (relative to the Playwright config directory), not a bare **`.auth/`** path.

**Do not:**

- Create **`turbo-flow`**, extra **`tests/a11y`** folders, or duplicate Playwright packages unless the team explicitly owns that layout.
- Edit **`.vscode/settings.json`** `nodePath` / `playwrightPath` unless **Diagnose** output tells you to.
- Patch or sideload a VSIX — use Marketplace **1.0.6** only.

---

## Section B — Extension (four gates)

Use the **Flow Runner** panel and **Command Palette** (`A11y Studio: …`). Panel **Expand all** / section chevrons should work on **1.0.6** — if a section stays closed, use **Expand all** on the view title bar or run the same action from the Command Palette.

| Gate | Pass criteria |
| --- | --- |
| **1. Diagnose** | Clean preflight; **`yarn a11y --list`** OK in Output; adopt-existing repair lines if config was wrong |
| **2. Spec discovery** | Flow Runner lists specs at the correct path; **`auth.setup.spec.ts`** is setup-only (not offered as a flow recording); Settings and Flow Runner agree on config path and spec count |
| **3. Run all flow tests** | Use **Run all flow tests (N specs)** at the top of the Flow tests section — runs **every** spec (not **Run this flow test**, which is one spec only). Repo or env failures are OK to report; extension must reach Playwright spawn (not “install Playwright” when workspace already has it) |
| **4. Record flow** | **Record flow** is available when the dev server URL is reachable (greyed = start dev server / VPN, not an extension bug) |

**Workspace scan (static lint):** **Activity Bar → Workspace scan** — **Scan all open packages** and **Scan active file** (in-tree rows and title-bar icons). Results appear in **Problems**.

**Safety:** Do not use **Remove A11y Studio setup** unless intentionally resetting. Cancel any destructive prompt you did not mean to open.

---

## Report back (redact secrets)

Paste to the maintainer via Teams/Slack:

1. Extension version from **Help → About** (expect **1.0.6**)
2. Output of **`yarn a11y --list`**
3. **`flowRunner`** block from **`a11y-studio.json`** (redact URLs if needed)
4. Full **Diagnose** output (**Output → A11y Studio Flow Runner**)
5. **Run all flow tests (N specs)** — pass/fail and first error line (not **Run this flow test** unless you are debugging one spec)
6. Verdict: **Section A** PASS/FAIL · **Section B** ___/4 · **Overall** PASS / PARTIAL / BLOCKED

Optional screenshots: Flow Runner panel (spec list + Playwright status), one failed run if any.

---

## Who fixes what

| Issue | Owner |
| --- | --- |
| Duplicate test titles, ESM setup spec, wrong `--project`, wrong `storageState` | Customer repo |
| Diagnose, panel tree, spec discovery, Playwright resolution inside the extension | A11y Studio vendor |
| Dev server down, VPN, greyed Record/Run | Environment / infra |

---

* [a11ystudio.io](https://a11ystudio.io) · Marketplace `a11ystudio.a11y-studio`*

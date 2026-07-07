# Enterprise adoption — client testing checklist

**Purpose:** Run on the **enterprise adoption laptop** (customer monorepo + VS Code). Copy this file locally or open the raw URL below. Fill in evidence sections and paste into your adoption smoke report.

**Raw URL (fetch on client machine):**

`https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-client-testing.md`

**Related (maintainer monorepo):** [enterprise-adoption architecture](https://github.com/a11ystudio/a11y-studio/blob/main/docs/specs/enterprise-adoption-architecture.md) · Marketplace extension: `a11ystudio.a11y-studio`

---

## Two layers (read first)

| Layer | What it is | Where fixes go |
| --- | --- | --- |
| **A11y Studio extension** | Panels, Diagnose, adopt-existing repair, spec discovery | Marketplace VSIX (A11y Studio team) |
| **Your Playwright suite** | `all-pages.spec.ts`, `auth.setup.spec.ts`, workspace `playwright.config.ts`, page data files | **Your monorepo** (adoption team) |

**Part A adoption passes only when both are healthy.** Extension bugs and spec/config bugs are different PRs in different repos.

---

## Extension versions

| Version | What to do on the laptop |
| --- | --- |
| **v1.0.5** (current Marketplace) | Fix **repo Playwright blockers** (Section A). Use **Command Palette** for Diagnose — panel Expand all is broken on 1.0.5. |
| **v1.0.6** (after publish / VSIX) | Re-run **Section B** — panel, Settings parity, Diagnose `--list` probe, setup specs excluded from flow list. |

Confirm installed version: **Extensions** → A11y Studio → version number.

---

## Section A — Repo fixes (do now on v1.0.5)

**System of record:** `yarn a11y --list` (or your repo’s equivalent `playwright test --list` script) must succeed **without** opening VS Code.

### A1. Duplicate test title (blocks `--list`, often shows 0 tests)

```bash
yarn a11y --list
# or from workspace root:
# npx playwright test --list --config playwright.config.ts
```

If output mentions **duplicate test title**:

1. Find the spec that generates duplicate titles (often an all-pages style spec driven by a shared page list).
2. Make every `test()` title **unique** (include path, role, or route segment in the title).
3. Re-run until `--list` completes with **≥ 1** test and no duplicate-title error.

### A2. `auth.setup.spec.ts` ESM loader

If you see **`ReferenceError: require is not defined`** at `auth.setup.spec.ts`:

1. Check Flow package or workspace `package.json` for `"type": "module"`.
2. Replace `require()` with `import` / documented ESM patterns in the setup spec.
3. Re-run `yarn a11y --list` until the setup file loads with no loader error.

### A3. Playwright project names

Read **workspace** `playwright.config.ts` → note `projects[].name` values.

- Do **not** assume `--project=chromium` unless your config defines a project named `chromium`.
- Update CI and local scripts to use your real names (e.g. `client`, `associate`, `shared`).

### A4. VS Code on v1.0.5 only (extension workarounds)

| Symptom on 1.0.5 | Action |
| --- | --- |
| Panel **Expand all** / chevrons do nothing | **Command Palette** → `A11y Studio: Diagnose Node & Playwright setup` |
| Settings shows wrong config or specs path | Trust **Diagnose Output** and terminal; ignore misleading Settings rows until v1.0.6 |
| PURGE input appeared accidentally | **Esc** / Cancel — nothing deletes until you type PURGE |
| Record / Run greyed out | Start dev server or VPN — environmental, not always a product bug |

Run **Diagnose once** after opening the Flow package (triggers adopt-existing auto-repair on v1.0.5).

---

## Section B — Part A gates (after repo fixes + target extension version)

Fill **Extension version** first, then run all four gates.

**Extension version tested:** `________` (Marketplace or VSIX)

**Date / tester:** `________`

### Gate 1 — Diagnose Node & Playwright

- [ ] **PASS** / [ ] **FAIL**
- Command Palette → `A11y Studio: Diagnose Node & Playwright setup`
- No dual-runtime warning after repair (nested vs workspace `@playwright/test`)
- `yarn a11y --list` succeeds in terminal

**Diagnose output** (paste from **Output → A11y Studio Flow Runner**; redact secrets and internal URLs):

```
[paste]
```

### Gate 2 — Spec discovery at package root

- [ ] **PASS** / [ ] **FAIL**
- `a11y-studio.json` → `flowRunner.testDir` matches where specs live (often `"."` at package root in adopt-existing)
- Workspace `playwright.config.ts` is used (not a superseded package-local studio config)
- Specs listed without moving files

**`flowRunner` block** (`a11y-studio.json` only; redact URLs and auth secrets):

```json
[paste]
```

### Gate 3 — Run flow tests (single runtime)

- [ ] **PASS** / [ ] **FAIL** / [ ] **ENV BLOCKED** (dev host down)
- Single `@playwright/test` runtime — no “Requiring @playwright/test second time”
- Run completes or fails only on environment (app not running), not config collision

**Evidence:**

```
[paste terminal or Output excerpt]
```

### Gate 4 — Record flow

- [ ] **PASS** / [ ] **FAIL** / [ ] **ENV BLOCKED**
- Record enabled when dev server is reachable
- New recordings respect configured test root

**Evidence:**

```
[paste]
```

---

## Copilot paste (customer monorepo)

Copy everything inside the fence into GitHub Copilot Chat in **your** monorepo.

```
Context: Enterprise adopt-existing monorepo. VS Code has A11y Studio Marketplace
(check Extensions for version — v1.0.5 vs v1.0.6).

Flow package: dedicated a11y-playwright/ (or team Flow folder). Workspace owns
playwright.config.ts and yarn/pnpm a11y scripts.

DO NOT fix A11y Studio extension UI on v1.0.5 — panel expand is a known bug.
Use Command Palette: "A11y Studio: Diagnose Node & Playwright setup".

Your job: fix Playwright suite blockers so `yarn a11y --list` lists tests.

1) Duplicate test title
   - Run: yarn a11y --list
   - If "duplicate test title" → fix duplicate routes/titles in all-pages spec / page list data.
   - Every test() title must be unique.

2) auth.setup.spec.ts ESM
   - If ReferenceError: require is not defined:
   - With "type": "module" in package.json → use import, not require().
   - Re-run yarn a11y --list until setup loads cleanly.

3) Playwright projects
   - Read workspace playwright.config.ts project names.
   - Use --project=<actual-name> in CI (not chromium unless defined).

4) Report back with:
   - yarn a11y --list full output
   - flowRunner block from a11y-studio.json (redact secrets)
   - Diagnose Output log (Command Palette, not panel tree)

Acceptance (repo phase on v1.0.5):
- yarn a11y --list succeeds
- auth.setup loads under ESM
- duplicate titles fixed
- correct --project names documented

After v1.0.6 ships: re-run Part A gates 1–4 from enterprise-client-testing.md Section B.
```

---

## Verdict (coordinator)

| Outcome | Check |
| --- | --- |
| [ ] **Repo ready** | `yarn a11y --list` passes; A2–A3 done |
| [ ] **Part A pass** | All four gates PASS (or ENV BLOCKED noted separately) |
| [ ] **Blocked** | List open FR IDs and owner (extension vs repo) |

**Open blockers:**

```
[paste]
```

---

## Terminal evidence log

```bash
# Run on adoption laptop — paste outputs below

yarn a11y --list

# Optional cross-check from workspace root:
# npx playwright test --list --config playwright.config.ts
```

**Output:**

```
[paste]
```

---

*Last updated: 2026-07-07 — v1.0.5 Marketplace + v1.0.6 queued. Maintainer: update this file when Part A gate wording changes.*

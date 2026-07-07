# Enterprise adoption — client testing checklist

**Purpose:** Run on the **enterprise adoption laptop** (customer monorepo + VS Code). Copy this file locally or open the raw URL below. Fill in evidence sections and paste into your adoption smoke report.

**Raw URL (fetch on client machine):**

`https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-client-testing.md`

**Public docs:** [a11ystudio.io — Enterprise adoption](https://a11ystudio.io/docs/enterprise-adoption/) · Marketplace: `a11ystudio.a11y-studio`

**Repo visibility:** This checklist lives in the **public** [`a11ystudio/media`](https://github.com/a11ystudio/media) repo. The product monorepo [`a11y-studio`](https://github.com/a11ystudio/a11y-studio) is **private** — adoption testers do not need access; the coordinator stores redacted evidence there.

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

## Section C — Report back to A11y Studio

When you finish a session, the coordinator needs a **short status** plus a **filled report**. Do not send raw customer repo code — only the evidence blocks below (redacted).

### What to send

| Item | Required? | Notes |
| --- | --- | --- |
| **One-line verdict** | Yes | PASS / PARTIAL / BLOCKED + extension version |
| **Filled report file** | Yes | Use [report template](./enterprise-client-testing-report-template.md) — save as `enterprise-client-testing-report-YYYY-MM-DD.md` |
| **This checklist** (optional) | If helpful | Only if you filled Section B inline here |
| **Screenshots** | Optional | Flow Runner panel after Diagnose; UI bugs only |

### How to send (pick what your team uses)

**Banking / locked-down environments:** GitHub Gist and **email** are often disabled. Use **Teams/Slack**, **internal chat**, or a **live session** — text paste beats screenshots.

| Channel | What to do |
| --- | --- |
| **Teams / Slack / internal chat** | Paste Evidence blocks + one-line verdict into a **private** DM (preferred when email is blocked). |
| **Cursor / live session** | Paste terminal + Diagnose text in chat; coordinator copies into GitHub smoke report. |
| **Email** | Subject = one-line verdict. Attach `.md` or paste Evidence in body (if allowed). |
| **Internal ticket** | Jira / ServiceNow — paste Evidence; put ticket ID in report header. |
| **Confluence / SharePoint** | Internal page link only. |
| **Your monorepo** | Commit under `docs/adoption/` — internal link only if policy allows. |
| **Coordinator GitHub** | You do **not** need write access — coordinator pastes into the [smoke report](https://github.com/a11ystudio/a11y-studio/edit/main/docs/ai/smoke-reports/2026-07-07-corporate-laptop-v1.0.5-retest.md). |

There is **no** public A11y Studio web paste form yet. Do **not** put customer data in public GitHub Issues.

1. **Do not** use public GitHub Issues on `a11y-studio` with customer names or internal URLs.
2. **Do not** rely on GitHub Gist if your org blocks it.

### Redaction (mandatory)

Before sending, remove or replace:

- Production / staging URLs and hostnames (use `https://local.dev.example.com/` class placeholders if needed)
- Auth cookies, tokens, client secrets, `.auth/` file contents
- Employee or customer names in paths or screenshots

### Short status messages (copy-paste)

**Repo phase done, waiting for v1.0.6:**

```
Adoption repo phase DONE — yarn a11y --list passes. A11y Studio still v1.0.5.
Ready for v1.0.6 VSIX / Marketplace for Part A gate retest.
Report: enterprise-client-testing-report-YYYY-MM-DD.md attached.
```

**Blocked on repo:**

```
Adoption BLOCKED (repo) — yarn a11y --list fails: [error one-liner].
Extension v____. Working on spec/config fix in our monorepo.
Report attached.
```

**Part A pass:**

```
Adoption Part A PASS — A11y Studio v____. Gates 4/4 (or N ENV BLOCKED).
yarn a11y --list OK. Report attached.
```

**Part A blocked (extension):**

```
Adoption Part A BLOCKED (extension) — A11y Studio v____. Gates __/4.
Top issue: [e.g. panel expand / Diagnose / dual runtime].
Report attached. Repo list: OK.
```

### What the coordinator does with your report

- Updates the maintainer smoke report in the A11y Studio monorepo (neutral copy — no customer branding)
- Routes **extension** failures to a VS Code hotfix / publish
- Confirms **repo** fixes stay in your monorepo — no action needed from A11y Studio on your Playwright files
- Replies with: ship version, VSIX link, or “re-run gate N after fix”

### Report template (download on laptop)

```bash
curl -o enterprise-client-testing-report-template.md \
  https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-client-testing-report-template.md
```

Fill → save as `enterprise-client-testing-report-YYYY-MM-DD.md` → send to coordinator.

### Where evidence lives (public vs private)

| Repo | Visibility | Who uses it |
| --- | --- | --- |
| **[a11ystudio/media](https://github.com/a11ystudio/media)** | **Public** | Generic checklists only — **no customer paste** |
| **a11y-studio** | **Private** | Maintainer only — smoke reports with redacted client evidence |
| **Your bank monorepo** | Internal | Your Playwright fixes |

### Paste directly on GitHub (maintainer only)

| Who | Access |
| --- | --- |
| **Adoption laptop tester** | **No** access to private `a11y-studio`. Send text via Teams / Slack / Cursor / internal ticket. |
| **A11y Studio coordinator** | **Yes** — edit smoke report in **private** `a11y-studio` → paste client evidence → commit (redacted). |

**Coordinator workflow (email/Teams blocked):**

1. Client pastes Evidence text in **Teams, Slack, or Cursor chat** (private).
2. Coordinator opens **private** `a11y-studio` smoke report on GitHub → **Edit** → paste → redact → commit.
3. Coordinator replies with verdict + next step.

**Do not** put customer-internal evidence in the **public** `a11ystudio/media` files.

---

*Last updated: 2026-07-07 — v1.0.5 Marketplace + v1.0.6 queued. Maintainer: update this file when Part A gate wording changes.*

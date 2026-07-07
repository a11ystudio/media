# Enterprise adoption — laptop testing brief

**Purpose:** Enterprise monorepo + A11y Studio Flow Runner adopt-existing validation. Open this page on the adoption laptop (no GitHub login required).

**Fetch URL:** `https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-adoption-laptop.md`

**Product docs:** [a11ystudio.io — Enterprise adoption](https://a11ystudio.io/docs/enterprise-adoption/) · Extension: `a11ystudio.a11y-studio`

---

## Before you start

1. Confirm **A11y Studio** version under **Extensions** (Marketplace).
2. Disable `ms-playwright.playwright` for this workspace → **Reload Window**.
3. Run **Diagnose** via **Command Palette** → `A11y Studio: Diagnose Node & Playwright setup` (not only the panel tree).

| Version | Notes |
| --- | --- |
| **v1.0.5** | Panel **Expand all** may not work — use Command Palette for Diagnose. |
| **v1.0.6+** | Panel parity + Diagnose `playwright test --list` probe. |

---

## Copilot paste (copy everything in the box)

Paste into **GitHub Copilot Chat** in your monorepo:

```
Enterprise adopt-existing monorepo. VS Code: A11y Studio from Marketplace (note version in Extensions).

Flow package: a11y-playwright/ (or team Flow folder). Workspace owns playwright.config.ts and yarn a11y scripts.

DO NOT fix A11y Studio extension UI on v1.0.5 — panel expand is a known bug. Use Command Palette: "A11y Studio: Diagnose Node & Playwright setup".

Fix Playwright suite blockers so yarn a11y --list lists tests:

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

4) When done, paste back in chat:
   - yarn a11y --list full output
   - flowRunner block from a11y-studio.json (redact secrets)
   - Diagnose Output log (Output → A11y Studio Flow Runner)
```

---

## Repo checks (terminal)

```bash
yarn a11y --list
```

| Error | Fix |
| --- | --- |
| Duplicate test title | Unique `test()` titles in spec / page list |
| `require is not defined` in auth.setup | ESM `import` when `"type": "module"` |
| Wrong `--project` | Match names in workspace `playwright.config.ts` |

---

## Part A gates

| # | Gate | Pass when |
| --- | --- | --- |
| 1 | **Diagnose** | PASS; no dual-runtime warning; `yarn a11y --list` OK |
| 2 | **Spec discovery** | `flowRunner.testDir` matches spec location; workspace config used |
| 3 | **Run flow tests** | Single Playwright runtime; env-only failures if host down |
| 4 | **Record flow** | Record works when dev server is up |

**Extension version:** __________  
**Date:** __________  
**Verdict:** PASS / PARTIAL / BLOCKED · **Score:** ___ / 4

### Evidence (paste in team chat — redact secrets)

**`yarn a11y --list`:**

```
[paste]
```

**Diagnose output:**

```
[paste]
```

**`flowRunner` block (`a11y-studio.json`):**

```json
[paste]
```

---

## Extension vs repo

| Symptom | Owner |
| --- | --- |
| Panel expand, Settings path mismatch, PURGE UX | A11y Studio extension |
| Duplicate titles, ESM auth.setup, wrong project | Your monorepo |
| Record/Run greyed out | Dev server / VPN (environment) |

---

*A11y Studio · Enterprise adoption validation · 2026-07-07*

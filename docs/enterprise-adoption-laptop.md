# Enterprise adoption — laptop testing brief

**Fetch (client laptop, no login):** `https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-adoption-laptop.md`

**GitHub view:** https://github.com/a11ystudio/media/blob/main/docs/enterprise-adoption-laptop.md

**Updated:** 2026-07-07 · Extension **v1.0.5** Marketplace

---

## Latest status — paste this summary to vendor chat

```
Adoption retest PARTIAL — v1.0.5 — Repo Section A PASS, Section B extension gates pending.

Section A (repo): PASS
- yarn -s a11y --list → Total: 39 tests in 2 files
- flowRunner: setupMode adopt-existing, testDir ".", playwrightConfigPath "../playwright.config.ts"
- Single @playwright/test runtime at workspace root (no nested duplicate under flow package)
- Repo fixes applied: duplicate enrollment test title; auth.setup ESM loader

Section B (extension gates 1–4): PENDING — need Diagnose Output + Run/Record evidence

Do NOT claim full Part A pass or migration-ready until Section B verified.
```

---

## Scorecard

| Item | Status | Notes |
| --- | --- | --- |
| **Section A — repo** | **PASS** | `yarn a11y --list` lists 39 tests |
| **A1 duplicate titles** | **PASS** | Page-list duplicate enrollment title fixed |
| **A2 auth.setup ESM** | **PASS** | `require` → `import` under `"type": "module"` |
| **A3 project names** | **PASS** | Use workspace config projects, not `chromium` |
| **Gate 1 Diagnose** | **PENDING** | Run via Command Palette; paste Output |
| **Gate 2 spec discovery** | **LIKELY PASS** | Config aligned — confirm in Diagnose |
| **Gate 3 Run** | **PENDING** | Needs dev host or note ENV BLOCKED |
| **Gate 4 Record** | **PENDING** | Needs dev host or note ENV BLOCKED |

**Verdict:** **PARTIAL** · **Part A score:** Section A done · **Gates:** ___ / 4

---

## Copilot paste — NOW (Section B only)

**Section A is done. Copy this block into Copilot Chat:**

```
Context: Enterprise adopt-existing monorepo. A11y Studio v1.0.5 Marketplace.
Section A (repo) is PASS — do not change specs unless Run fails on spec errors.

Confirmed baseline:
- yarn -s a11y --list → 39 tests in 2 files
- flowRunner.setupMode: adopt-existing, testDir: ".", playwrightConfigPath: "../playwright.config.ts"
- Single @playwright/test at workspace root (no nested duplicate under flow package)

Your job: Section B extension gates only.

1) Command Palette → "A11y Studio: Diagnose Node & Playwright setup"
   Paste full Output log here (redact internal URLs). Gate 1 = PASS/FAIL.

2) Confirm spec discovery (Gate 2): testDir and workspace playwright.config alignment in a11y-studio.json.

3) Gate 3 — Run one flow test if dev server reachable. PASS / FAIL / ENV BLOCKED.
   If dev host down, say ENV BLOCKED — do not treat as extension P0.

4) Gate 4 — Record flow if dev server up. PASS / FAIL / ENV BLOCKED.

DO NOT fix extension panel UI on v1.0.5 (panel expand known bug — Diagnose via Command Palette only).

Report back with Gate 1–4 table + pasted Diagnose output + yarn a11y --list (already passing).
Do not claim migration-ready or full Part A pass until all four gates have evidence.
```

---

## Copilot paste — DONE (Section A — keep for reference)

```
Enterprise adopt-existing monorepo. VS Code: A11y Studio v1.0.5 Marketplace.

Flow package at package root. Workspace owns playwright.config.ts and yarn a11y scripts.

Fix Playwright blockers so yarn a11y --list lists tests:

1) Duplicate test title — make every test() title unique in page-list / all-pages spec.
2) auth.setup ESM — replace require() with import when package.json type is module.
3) Playwright projects — read workspace config project names; fix --project in scripts.

STATUS: COMPLETE as of 2026-07-07 — 39 tests listed.
```

---

## Evidence log (fill as you go)

### `yarn a11y --list` — PASS (2026-07-07)

```
Total: 39 tests in 2 files
(paste full output below if vendor needs it)
```

```
[paste full terminal output — redact paths if required]
```

### `flowRunner` block — aligned

```json
{
  "flowRunner": {
    "setupMode": "adopt-existing",
    "testDir": ".",
    "playwrightConfigPath": "../playwright.config.ts"
  }
}
```

(paste actual block from a11y-studio.json — redact URLs/secrets)

### Diagnose output — Gate 1 (PENDING)

```
[paste Output → A11y Studio Flow Runner]
```

### Gate 3 Run / Gate 4 Record (PENDING)

```
[paste or "ENV BLOCKED — dev host unreachable"]
```

---

## Part A gate definitions

| # | Gate | Pass when |
| --- | --- | --- |
| 1 | **Diagnose** | PASS; no dual-runtime warning; `yarn a11y --list` OK |
| 2 | **Spec discovery** | `flowRunner.testDir` matches spec location; workspace config used |
| 3 | **Run flow tests** | Single Playwright runtime; env-only failures if host down |
| 4 | **Record flow** | Record works when dev server is up |

---

## v1.0.5 workarounds

| Issue | Workaround |
| --- | --- |
| Panel Expand all broken | Command Palette → Diagnose |
| Settings path mismatch | Trust Diagnose + terminal until v1.0.6 |
| Record/Run greyed | Start dev server / VPN |

---

## Extension vs repo

| Symptom | Owner |
| --- | --- |
| Panel expand, Settings path, PURGE UX | Extension (v1.0.6 fix queued) |
| Duplicate titles, ESM auth.setup | Repo (**done**) |
| Record/Run greyed | Environment |

---

*Temporary public copy for adoption laptop · Remove from media repo when retest completes*

# a11ystudio/media

Public brand and marketing assets for [A11y Studio](https://a11ystudio.io). Single source of truth for logos and Marketplace screenshots.

## Layout (mirror this tree locally)

```
brand/
  icon.svg       # Canonical logo source (Figma export)
  icon-128.png   # VS Code Marketplace icon + website header (128×128)
  icon-512.png   # Marketing / high-res (512×512)
screenshots/     # VS Code UI captures for README / Marketplace Details
docs/
  enterprise-client-testing.md           # Adoption laptop checklist + Copilot paste (client machines)
  enterprise-client-testing-report-template.md   # Fill in and send back to coordinator
```

## URLs

Stable raw links (replace `main` with a tag when pinning releases):

- Logo: `https://raw.githubusercontent.com/a11ystudio/media/main/brand/icon-128.png`
- Screenshots: `https://raw.githubusercontent.com/a11ystudio/media/main/screenshots/<filename>`
- **Enterprise client testing:** `https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-client-testing.md`
- **Retest report template (send back):** `https://raw.githubusercontent.com/a11ystudio/media/main/docs/enterprise-client-testing-report-template.md`

## How products use this repo

| Product | Uses |
|---------|------|
| **a11ystudio.io** | Logo URL above (no file copy in the monorepo) |
| **VS Code extension** | `pnpm run sync:media` in [`a11y-studio`](https://github.com/a11ystudio/a11y-studio) copies `brand/` → `apps/vscode-extension/media/` for the VSIX |
| **Marketplace README** | `screenshots/` via `raw.githubusercontent.com` URLs |
| **Enterprise adoption laptop** | [`docs/enterprise-client-testing.md`](docs/enterprise-client-testing.md) — run checklist; [`enterprise-client-testing-report-template.md`](docs/enterprise-client-testing-report-template.md) — fill and send back |

**To change the logo:** edit `brand/icon.svg` here, regenerate PNGs (`icon:render` in the monorepo), commit and push **this repo**. The website updates without redeploying the code monorepo.

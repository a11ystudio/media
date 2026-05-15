# a11ystudio/media

Public brand and marketing assets for [A11y Studio](https://a11ystudio.io). Single source of truth for logos and Marketplace screenshots.

## Layout (mirror this tree locally)

```
brand/
  icon.svg       # Canonical logo source (Figma export)
  icon-128.png   # VS Code Marketplace icon + website header (128×128)
  icon-512.png   # Marketing / high-res (512×512)
screenshots/     # VS Code UI captures for README / Marketplace Details
```

## URLs

Stable raw links (replace `main` with a tag when pinning releases):

- Logo: `https://raw.githubusercontent.com/a11ystudio/media/main/brand/icon-128.png`
- Screenshots: `https://raw.githubusercontent.com/a11ystudio/media/main/screenshots/<filename>`

## Monorepo sync

In [`a11y-studio`](https://github.com/a11ystudio/a11y-studio), run from repo root:

```bash
git submodule update --init media
pnpm run sync:media
```

That copies `brand/` into the extension and website build inputs. Do not edit copies in the monorepo without updating this repo first.

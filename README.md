# emberry · brand previews

Static, self-contained mockups used to show a prospect the emberry platform
**in their own branding** before any onboarding. Served via GitHub Pages.

## Structure

```
/                       → neutral splash (no prospect is listed here)
/<prospect-slug>/       → that prospect's preview (index.html)
```

Each preview is a single, dependency-free `index.html` (fonts load from Google
Fonts over CDN). Share the per-prospect URL directly:

```
https://<user>.github.io/emberry-previews/<prospect-slug>/
```

## Add a new prospect

1. Copy an existing folder (e.g. `green-leaves/`) to `<new-slug>/`.
2. In `<new-slug>/index.html`, change the brand in these spots:
   - **Colours** — the `--tenant-primary` and `--tenant-accent` CSS tokens in `:root` (single source).
   - **Name** — the `.legal` text in the app header.
   - **Logo** — the mark SVG in the app header.
   - **Copy** — the survey wording (headings, area names, intro) to fit their vertical.
3. Commit and push. Pages redeploys automatically.

## Notes

- This repo is intentionally separate from the product codebase.
- The root `index.html` does not enumerate prospects; only someone with a
  direct link sees a given preview.

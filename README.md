# emberry · brand previews

Static, self-contained mockups used to show a prospect the emberry platform
**in their own branding** before any onboarding. Served via GitHub Pages on a
branded custom domain.

## Structure

```
/                       → neutral splash (no prospect is listed here)
/<prospect-slug>/       → that prospect's preview (index.html)
```

Each preview is a single, dependency-free `index.html` (fonts load from Google
Fonts over CDN). Share the per-prospect URL directly:

```
https://preview.emberry.com.au/<prospect-slug>/
```

The site is published at **`preview.emberry.com.au`** — a GitHub Pages custom
domain (see the root `CNAME` file), HTTPS enforced. The old
`https://d0199.github.io/emberry-previews/<prospect-slug>/` links still resolve
and 301-redirect to the branded domain.

## Vertical comes first

**Pin the prospect's vertical before you build the page** (aged care, childcare,
GP/medical, …). It is not cosmetic — the vertical drives two concrete things:

- **Design & copy** — survey questions, area labels, probe chips and microcopy
  must read natively for that sector. e.g. aged care asks about *"your loved
  one"* and the *care team*; childcare asks about *"your child"* and
  *educators*. Never ship one vertical's wording under another vertical's brand.
- **The emberry logo link** — every page carries an emberry logo at the top that
  links to `https://www.emberry.com.au/industries/<vertical>` (e.g.
  `/industries/aged-care`). The slug must be a real industry page on
  emberry.com.au, and the correct one for that prospect.

So a wrong/loose vertical doesn't just misword the survey — it points the header
logo at the wrong (or a 404) industry page.

## The emberry logo header

Each preview opens with a clickable emberry mark + wordmark (`.topbar` /
`.site-logo` near the top of `<body>`) linking to the vertical's industry page.
`st-vincents-care/` is the current reference implementation — copy its `.topbar`
block and `.site-logo` CSS into any older preview that predates this.

## Add a new prospect

1. Copy an existing folder **of the same vertical** (e.g. `emberry-agedcare/`,
   or `st-vincents-care/` for the full layout with the logo header) to
   `<new-slug>/`.
2. In `<new-slug>/index.html`, change the brand in these spots:
   - **Colours** — the `--tenant-primary` and `--tenant-accent` CSS tokens in `:root` (single source).
   - **Name** — the `.legal` text in the app header.
   - **Logo** — the mark SVG in the app header.
   - **emberry logo link** — the `.site-logo` anchor `href` at the top of the
     page → `https://www.emberry.com.au/industries/<vertical>`.
   - **Copy** — the survey wording (headings, area names, probe chips, intro) to
     fit their vertical.
3. Commit and push. Pages redeploys automatically to
   `https://preview.emberry.com.au/<new-slug>/`.

> **Don't substitute the location/prospect name into generic microcopy.** Some
> lines are deliberately generic and must stay that way — e.g. the **NFC tags**
> caption reads "…around your **facility**.", not "…around your *Hamersley*."
> Replace branding (name, logo, colours) and vertical-specific survey wording
> only; leave generic nouns like "facility" alone.

## Notes

- This repo is intentionally separate from the product codebase.
- The root `index.html` does not enumerate prospects; only someone with a
  direct link sees a given preview.

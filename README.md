# emberry · brand previews

Static, self-contained mockups used to show a prospect the emberry platform
**in their own branding** before any onboarding. Served via GitHub Pages on a
branded custom domain.

## Structure

```
/                       → neutral splash (no prospect is listed here)
/<prospect-slug>/       → that prospect's preview (index.html + admin/ images)
```

Each preview is a single `index.html` (fonts load from Google Fonts over CDN; a
tiny inline script drives the side-nav) plus an `admin/` image folder. Share the
per-prospect URL directly:

```
https://preview.emberry.com.au/<prospect-slug>/
```

The site is published at **`preview.emberry.com.au`** — a GitHub Pages custom
domain (see the root `CNAME` file), HTTPS enforced. The old
`https://d0199.github.io/emberry-previews/<prospect-slug>/` links still resolve
and 301-redirect to the branded domain.

## The reference template

**`st-vincents-care/` is the current reference — copy it for any new prospect.**
It is the full, up-to-date format; older folders (`green-leaves/`, `keiki/`, …)
predate parts of it. A complete preview now has, top to bottom:

1. **emberry logo header** (`.topbar` / `.site-logo`) — links to the vertical's industry page (see *Vertical comes first*)
2. **Left jump-to side-nav** (`.sidenav`) — sticky on desktop, hidden on tablet/mobile; a small inline scroll-spy script highlights the current section
3. **Survey journey** (`#journey`) — the phone-screen walkthrough of the respondent flow, ending on the thank-you / consent screen
4. **Kiosk preview** (`#kiosk`) — the on-site iPad/kiosk loop
5. **More ways to ask** (`#channels`) — QR poster, email, newsletter, SMS, NFC, website widget, social
6. **Testimonials wall** (`#testimonials`) — the public-reputation wall
7. **User admin** (`#admin`) — "behind the scenes" admin screenshots

Keep the side-nav links and section `id`s in sync. If a section isn't built yet
(e.g. admin before its screenshots exist), mark that nav link `disabled` with a
"soon" tag instead of linking to a missing anchor.

## Vertical comes first

**Pin the prospect's vertical before you build the page** (aged care, childcare,
GP/medical, …). It is not cosmetic — the vertical drives two concrete things:

- **Design & copy** — survey questions, area labels, probe chips and microcopy
  must read natively for that sector. e.g. aged care asks about *"your loved
  one"* and the *care team*; childcare asks about *"your child"* and
  *educators*. Never ship one vertical's wording under another vertical's brand.
- **The emberry logo link** — the header logo links to
  `https://www.emberry.com.au/industries/<vertical>` (e.g. `/industries/aged-care`).
  The slug must be a real industry page on emberry.com.au, and the correct one
  for that prospect.

So a wrong/loose vertical doesn't just misword the survey — it points the header
logo at the wrong (or a 404) industry page.

## Conventions (don't skip these)

- **Label seeded data as a mock-up.** Where a section is filled with test /
  seeded data (the testimonials wall, the admin screenshots), the copy must say
  so — e.g. *"a mock-up … using test data"*, *"shown with test data"*. Never
  imply seeded content is real customer data.
- **Real survey URL + real QR.** The channel CTAs (email, newsletter, SMS,
  follow-up) and the QR poster must point at the prospect's actual survey link
  (`https://staging.emberry.com.au/f/<site>/<link>`). Generate the QR for real
  (the `qrcode` npm package, SVG output), recolour the modules to the brand plum
  `#2D1F36`, and inline it — never leave the decorative placeholder QR.
- **Testimonials = consent.** The wall only shows reviews the respondent opted in
  to share. The end-of-survey thank-you screen carries that optional
  authorisation ("Happy for us to share your words?" → "Yes, you can feature my
  words"); keep the wall copy and that step consistent.
- **Admin screenshots: capture full-height.** The admin UI has a fixed sidebar,
  so a plain full-page screenshot paints it once and leaves a broken empty strip
  below. Capture by **growing the browser viewport to the full page height first,
  then shooting the viewport** (not full-page), at ~1440px × 2 → 2880px wide, into
  `<slug>/admin/` (`regulator.png`, `overview.png`).

## Add a new prospect

1. Copy `st-vincents-care/` (same vertical preferred) to `<new-slug>/`, including
   its `admin/` images as placeholders to replace.
2. In `<new-slug>/index.html`, change the brand in these spots:
   - **Colours** — the `--tenant-primary` and `--tenant-accent` CSS tokens in `:root` (single source).
   - **Name** — the `.legal` text in the app header.
   - **Logo** — the mark SVG in the app header.
   - **emberry logo link** — the `.site-logo` `href` → `…/industries/<vertical>`.
   - **Side-nav** — the `.sn-head` label; leave the section links unless you rename/drop sections.
   - **Copy** — survey wording (headings, area names, probe chips, intro) for the vertical.
   - **Survey URL + QR** — the channel CTA `href`s and the real QR (see *Conventions*).
   - **Testimonials** — swap the wall cards for the prospect's reviews; keep the consent framing and the test-data label.
   - **Admin** — replace `admin/*.png` with the prospect's captures (full-height; see *Conventions*).
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

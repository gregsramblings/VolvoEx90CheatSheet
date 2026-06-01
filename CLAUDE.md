# CLAUDE.md

Operating notes for agents working in this repo. See `README.md` for the fuller project write-up.

## What this is

A single-page, print-optimized **Volvo EX90 owner's cheat sheet**. It is a static
design artifact, not an application — there is no build step, no dependencies, no
server, and no tests.

## Files

- **`volvo-ex90-cheat-sheet.html`** — the editable source and the **only file you
  edit**. Self-contained: inline `<style>`, no external assets or scripts. The top
  of the file has an inline guide explaining cards, colors, badges, and callouts.
- **`volvo-ex90-cheat-sheet.pdf`** — print-ready export, paginated to one page.
  A generated artifact; never hand-edit. Regenerate from the HTML (see below).
- **`volvo-ex90-cheat-sheet.png`** — preview image embedded in the README. Also
  generated; refresh if the design changes materially.
- **`README.md`** — project notes, design decisions, and revision instructions.

## How it's structured

- Seven procedure **cards**, each `<article class="card card--COLOR">`.
- Cards are grouped into three `<div class="pcol">` columns, balanced for roughly
  equal height — this is what makes the one-page print fit work.
- A `@media print` block at the end of the CSS switches the dark on-screen theme to
  a light, ink-friendly, single **US Letter landscape** page.

## Editing rules (important, learned the hard way — see README "Decisions & notes")

- After any content change, **print-preview (Cmd/Ctrl-P → Landscape)** and confirm it
  still fits **one page**. If you add or lengthen a card, rebalance by moving cards
  between the three `.pcol` columns.
- Keep **print-only accents solid**, not gradients: `.card::before` and
  `ol.steps>li::after` are forced to solid colors in `@media print` because CSS
  gradients export as slow, bulky PDF "pattern" objects.
- Do **not** put an inline `color` on the software-version range in the header — an
  inline white color once made it invisible on the white printed page. Set colors via
  CSS only.
- Update the **version / date / URL** in the `<header>` for each revision.

## Regenerating the PDF/PNG

There is no script. Open the HTML in a browser, print to PDF (Letter, Landscape) to
refresh the PDF; re-export/screenshot for the PNG. Do not edit those binaries directly.

## Related

- Blog post: <https://gregwilson.tech/reboot-volvo-ex90>
- Remote: `github.com/gregsramblings/VolvoEx90CheatSheet`
- Software versions covered: 1.2.15 – 2.1.26 (in-card notes referencing **1.3.18** are
  version-specific and intentionally left as-is).

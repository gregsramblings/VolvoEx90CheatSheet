# Volvo EX90 Cheat Sheet — Project Notes

A redesign of the Volvo EX90 owner's cheat sheet: modern, colorful, easy to read,
editable for future revisions, and optimized to print on a single page.

## Blog post

There is a corresponding blog post at <https://gregwilson.tech/reboot-volvo-ex90> that
includes a responsive HTML version and a printable PDF version of the cheat sheet.

## Files

- **volvo-ex90-cheat-sheet.html** — the editable source. This is the file to edit.
  - On screen: a dark, colorful, three-column responsive layout.
  - When printed (Cmd/Ctrl-P → **Landscape**): automatically switches to a light,
    ink-friendly layout that fits **one Letter landscape page**.
- **volvo-ex90-cheat-sheet.pdf** — the print-ready export (already paginated to one page).
  Regenerate it after edits by opening the HTML in a browser and printing to PDF.
- **cheat-sheet-1.3.18.jpg** — the original design (source for content).
- **The Volvo EX90 Cheat Sheet for 1.3.18.pptx** — the original PowerPoint version.

## How it's built

- Seven procedure "cards," each an `<article class="card card--COLOR">` block.
- Cards are grouped into three `<div class="pcol">` columns. The grouping is chosen so
  the columns are roughly equal height, which is what makes the one-page print fit work.
  - Column 1: Reboot Central Computer · Restore Google Maps & Assistant
  - Column 2: Reset UWB Digital Key Module · Full Factory Reset
  - Column 3: Fix Speed-Limit Indicator · Reboot Displays · Dog Mode
- A `@media print` block at the end of the CSS handles the light, compact, single-page layout.

## How to revise

1. Edit text inside the relevant `<article>` in the HTML (the top of the file has an
   inline guide explaining cards, colors, badges, and callouts).
2. Update the **version / date / URL** in the `<header>` for each revision.
3. If you add or substantially lengthen a card, move cards between the three
   `<div class="pcol">` columns to keep them balanced.
4. Print-preview (Cmd/Ctrl-P, Landscape) to confirm it still fits one page, then
   print-to-PDF to refresh the PDF.

## Decisions & notes

- Content was cross-checked against the PowerPoint. One fix: the PARK button is at the
  **"end of the gear selector"** (matching the PPT).
- The print version hides the large corner card-numbers, so cross-references were changed
  from "(card 1)" / "(card 4)" to the procedure names.
- The on-screen legend explaining the badges is hidden in print (each badge is already
  self-labeled) to save vertical space and keep it to one page.
- The software-version range in the header (`<strong>` inside `.meta`) must NOT carry an
  inline `color` — an inline white color once made it invisible on the white printed page.
  Colors are now set via CSS (white on the dark screen theme, dark blue in `@media print`).
- Print performance: CSS gradients become PDF "pattern" objects, which made the exported
  PDF slow to render. In the `@media print` block the card top-bar (`.card::before`) and the
  step connector lines (`ol.steps>li::after`) are forced to **solid** colors. This removed
  all gradient patterns (75 → 0) and shrank the PDF (~152 KB → ~107 KB) with no visible
  change. Keep print-only accents solid if you add more cards.

## Open item

- **A4 support:** the print layout is tuned for US Letter landscape. If you ever need A4,
  ask and it can be adjusted (or use the browser's "Fit to page" / "Scale" option when printing).

## Software versions covered

1.2.15 – 2.1.26.

(The in-card notes that mention **1.3.18** specifically refer to behavior observed on
that version and are intentionally left as-is.)

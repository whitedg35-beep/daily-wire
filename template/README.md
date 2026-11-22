# The Newspaper Template — Pieces and a Package

## First principle

**The box stays. You just change the pieces.**

Every issue of either paper is built the same way: a fixed frame (the box)
that never changes, filled with swappable pieces. A new issue is never a
rebuild — it is the same box with new pieces dropped in. The color scheme
is a piece too.

## The package

```
template/
  daily-wire-newspaper.html     assembled sample — THE DAILY WIRE, No. 2
  whited-daily-newspaper.html   assembled sample — THE WHITED DAILY, roll call
  frame/
    daily-wire-frame.css        the box, Daily Wire edition (structure only)
    whited-daily-frame.css      the box, Whited Daily edition (structure only)
    daily-wire-frame.html       empty box with marked piece drop zones
    whited-daily-frame.html     empty box with marked piece drop zones
  pieces/
    piece-headline.html         banner headline + standfirst
    piece-article.html          one story block (headline + paragraphs)
    piece-caption.html          the one-line caption under a card slot
    piece-hero-ticket.html      the sideways hero ticket
    piece-card-slot.html        the upright card slot
  schemes/
    wire-pink-teal.css          newsprint, charcoal, pink/teal rules, gold hero
    full-gold.css               foil takes the whole page
    marble-gold-silver.css      marble ground, gold foil, silver trim
    whited-silver-brass.css     silver/platinum + brass/champagne (Whited home)
    custom-scheme.css           blank starter — copy it, rename it, recolor it
```

### What's the box

The frame: page border and trim, masthead block, sub-banner, the article
grid (three columns, thin dividers), the bottom strip, and the footer —
plus the styling hooks every piece hangs on. Frame files are marked
`FRAME: do not edit per issue`. If a change is needed in the frame, it is
a template change, made once, for every future issue — never an issue edit.

### What the pieces are

Pieces are small standalone HTML snippets in `pieces/`. Each carries a
comment header naming the piece and the drop zone it belongs in. Pieces
hold **content only** — headline text, article text, caption text, the
ticket's face text. All styling lives in the frame CSS and the scheme;
pieces never carry inline styles, so the same piece drops into either
edition's box and wears that box's skin.

In the assembled files, frame and pieces are marked in comments:
`<!-- FRAME: ... -->` vs `<!-- PIECE: headline -->`,
`<!-- PIECE: article -->`, `<!-- PIECE: card slot content -->`, and so on.

### The scheme is a piece

**The scheme is a piece. Change it per situation; the box doesn't care.**

Each file in `schemes/` defines the same set of CSS variables — ink,
paper, rules, banner, hero face, slot trim, all of it. An edition swaps
its scheme by changing one `<link>` line. Frame untouched, pieces
untouched. Launch day can run `full-gold`; a normal day runs
`wire-pink-teal`; the personal paper runs `whited-silver-brass`.
Slot dimensions are deliberately **not** scheme variables — size is
frame law, not taste.

## The spec

- **Page:** US Letter, 8.5 × 11 in. `@page { size: letter; margin: 0.4in }`,
  content box 7.7 × 10.2 in, `print-color-adjust: exact`. Print at 100%.
- **Card slot (upright):** exactly **2.5in × 3.5in** (63.5 × 88.9 mm) —
  the standard trading/playing card. Drawn as a ticket frame: perforation
  stub along the bottom, ADMIT ONE in the stub. Two per page, in the left
  and right grid columns, each followed by a caption piece.
- **Hero slot (sideways):** exactly **3.5in wide × 2.5in tall** — the
  standard card turned sideways, a real ticket's natural shape.
- **Slot variants** (for physical cards on the printed page):
  cut the card at **2.55 × 3.55 in** for bleed/glue-on, or open a
  **2.4 × 3.4 in** window in the page for slide-behind. Sideways hero,
  same logic: 3.55 × 2.55 in glue-on, 3.4 × 2.4 in window.

### The sideways-hero rule

**The ticket lays in front as the main thing when it's sideways.**
Every page leads with the hero ticket: landscape, front and center,
laid over the top of the article grid like it was set down on the paper —
a whisper of shadow, one degree of rotation, print-clean. It carries the
LIVE WIRE TICKET™ face treatment and the issue's main headline. The two
upright card slots are secondary seats. Never lead with an upright slot;
the sideways ticket is the front door of the page.

### Type

System fonts only — nothing hotlinked, nothing loaded from a CDN.

- **Masthead:** blackletter stack (`"Old English Text MT", "Cloister Black",
  "UnifrakturMaguntia",` then heavy serif fallbacks). On a machine with no
  blackletter face installed, the render falls back to a heavy serif
  (locally: Noto Serif Display Black) — the layout does not depend on it.
- **Headlines:** condensed black sans stack (Anton / Bebas Neue / Impact /
  Noto Sans Display), all caps.
- **Body:** Georgia / Noto Serif, justified, narrow columns.

## How to produce an issue

1. Copy the edition's frame skeleton (`frame/*-frame.html`) or the last
   assembled issue.
2. Pick the scheme for the situation; set the `<link>` to it.
3. Swap the pieces: new banner headline + standfirst, new hero-ticket
   face (headline, ticket number, meta), articles, captions. Change the
   issue line in the sub-banner. Touch nothing marked FRAME.
4. Render at 100%:
   - PDF: headless Chromium `--print-to-pdf` with `--no-pdf-header-footer`.
   - PNG preview: screenshot at window 816×1056 with device scale 1.5625
     (= 1275×1650 px, a 150 DPI page).
5. Read the render before it ships: masthead spelling, headline spelling,
   footer line. The box guarantees the shape; a human guarantees the words.

## Verified on the samples (Nov 22, 2026)

Both assembled samples were rendered and measured:

- PDFs: exactly **1 page**, page size **612 × 792 pt** (US Letter).
- PNG measurement at 150 DPI (2.5in = 375px, 3.5in = 525px), slots and
  hero painted solid and bounded:
  - Daily Wire — hero **525 × 375 px = 3.500 × 2.500 in**;
    slots **375 × 525 px = 2.500 × 3.500 in** (both).
  - Whited Daily — hero **525 × 375 px = 3.500 × 2.500 in**;
    slots **375 × 525 px = 2.500 × 3.500 in** (both).
- Mastheads read exactly THE DAILY WIRE / THE WHITED DAILY; headlines are
  the papers' own (No. 2's "THE BRIDGE DOESN'T CONNECT" leads the sample);
  no placeholder text anywhere; no other paper's name or styling is used —
  the layout mechanics are the only borrowed idea, and the design is ours.

## Ownership

The newspaper template — both editions' frames, the ticket-slot frames,
the sideways hero treatment, the pieces system, and the schemes — is a
design of the house. **© Bumkus IP · Licensed, never sold — see the
repository LICENSE.** The papers are ours: The Daily Wire is Vice City
Wire's newspaper; The Whited Daily is Garrett Whited's personal paper.

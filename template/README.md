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
  PLUG-IN.md                    THE CONTRACT — slots, piece rules,
                                frame-exactness, surface-independence
  daily-wire-newspaper.html     assembled sample — THE DAILY WIRE, No. 2
  whited-daily-newspaper.html   assembled sample — THE WHITED DAILY, roll call
  frame/
    daily-wire-frame.css        the box, Daily Wire edition (structure only)
    whited-daily-frame.css      the box, Whited Daily edition (structure only)
    daily-wire-frame.html       empty box with marked piece drop zones
    whited-daily-frame.html     empty box with marked piece drop zones
  pieces/                       every piece, indexed in pieces/MANIFEST.md
    piece-headline.html         banner headline + standfirst
    piece-article.html          one story block (headline + paragraphs)
    piece-caption.html          the one-line caption under a card slot
    piece-text-post.html        a text post — content only, any text zone
    piece-hero-ticket.html      the sideways hero ticket
    piece-winning-ticket.html   the winning ticket — the face states the win
    piece-card-slot.html        the upright card slot
    piece-coin-insert.html      the coin's face — drops into the coin base
  formats/                      the same schema, other shapes — see Formats
    poster/                     full-page Letter portrait, one big hero
    square/                     1:1, 1080 x 1080 — feed posts
    vertical/                   9:16, 1080 x 1920 — stories / reel covers
    banner/                     wide 3:1, 1584 x 528 — profile / group covers
    coin/                       the Token — base is the box, face is a piece
    coin-opener/                the waking coin — the seven-beat opener
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

## Formats — one schema, many shapes

The schema is one system: **box, pieces, schemes — and now formats.**
A format is just another box, shaped for a situation. Every format in
`formats/` is built the same way as the newspaper: a frame CSS + frame
skeleton with the same FRAME / PIECE comment discipline, the same
pieces from `pieces/`, and the same scheme contract — any format
accepts any scheme file by link swap, frame and pieces untouched.

**A new situation = pick a format, pick a scheme, swap the pieces.**

- **Poster** (`formats/poster/`) — full-page US Letter portrait. One
  banner headline, ONE BIG hero ticket sideways in front (the ticket
  face scaled up for display, 7:5 ratio preserved), one caption.
- **Square** (`formats/square/`) — 1:1, 1080 × 1080 design units, for
  feed posts. Headline above, hero ticket sideways centered, caption
  below.
- **Vertical** (`formats/vertical/`) — 9:16, 1080 × 1920, for stories
  and reel covers. Masthead strip at the top, hero ticket sideways in
  the upper third, headline and article stacked under it.
- **Banner** (`formats/banner/`) — wide 3:1, 1584 × 528, for profile
  and group covers. Masthead rides left with the headline under it,
  hero ticket sideways in front on the right.
- **Coin** (`formats/coin/`) — the Token. See below.
- **Coin-opener** (`formats/coin-opener/`) — the waking coin. See below.

**The plug-in contract** (`PLUG-IN.md`) governs all of it: every
slot's dimensions, the piece rules (content only, no color, no
dimensions), the three layers (surface → scheme mask → piece),
and the **frame-exactness rule** — plugging in a new piece
changes only the piece, and the reels must represent the frame
exactly. **The package is live as-is: plug the piece in, replace
the outer reel, nothing else moves.**

### The coin

**The coin is a box too — the base stays, the insert changes.**

The coin is the opposite of the ticket: where a ticket can't fit, the
coin carries the mark. Same schema, round:

- **The BASE is the box (FRAME).** A round blank with a reeded edge, a
  raised rim, and the LIVE WIRE TICKET™ mark placement struck into the
  rim — the house mark at the top placement, the house name at the
  bottom. The base never changes between strikes.
- **The FACE is a piece (PIECE: coin-insert).** Different faces drop
  into the same base: a **Wire face** (the house's own coin), a
  **recipient face** (a name and handle, struck for one person), an
  **issue face** (a headline and number for a big issue). One base,
  many inserts.
- **The scheme is the metal.** Swap the scheme link and the same base
  is struck in another metal — full gold, marble, silver-brass —
  frame and insert untouched.

**Presentation direction.** The physical inspiration is Garrett's own
collection — a gold Buffalo-style round and PCGS-slabbed proofs: the
coin presented seated in a slab, label on top, one face showing. The
digital sample follows that presentation: a label strip, the coin
seated center on the card, a caption under it. **Digital spec only for
now** — no physical strike is specified here.

**The color rule (Garrett, Nov 22, 2026).** Inserts and renders use
ONLY the house scheme variables (`wire-pink-teal`, `full-gold`,
`marble-gold-silver`, `whited-silver-brass`) and our own mark work.
The collection photos are presentation inspiration ONLY — the
slab/insert idea. **No real coin's artwork is reproduced** — no
Buffalo, no US Mint design, nothing borrowed. The coin face is our
LIVE WIRE TICKET™ mark in our colors, and that is what makes it ours.

### The coin-opener

**The opener is a format too — a box that runs in time.**

The coin-opener is the house's opening sequence, seven beats,
always in this order (the beat law lives in
`formats/coin-opener/coin-opener-frame.css`):

1. **WAKE** — the newspaper page fills the frame; a shadow
   sweeps over it, dream-quick — *where am I?*
2. **FALL** — the coin, resting on the page, falls into its
   place on the page and settles.
3. **ROLL** — the gold coin rolls in, the batch roll, real
   spin depth, drumroll under it.
4. **TRANSFORM** — mid-turn, shaking, the gold becomes the
   white marble coin.
5. **FACE FALL** — the face falls down into the medallion; the
   opening says the name.
6. **POP** — the coin pops toward the viewer and opens into
   the **square**; the outer reel plays inside the reel slot.
7. **BACK LINE** — "THE WIRE CARRIED IT LIVE · PASS THIS
   TICKET ON · @vicecitywire92."

Every beat carries pieces, not edits: the newspaper issue, the
coin insert, the face, and the outer reel all plug in under the
contract in `PLUG-IN.md`. The white coin is the one people learn
to touch — the opener is built so the tap lands on it.

### Piece types

Beyond the newspaper's own pieces, two piece types are named
citizens of the schema (both in `pieces/`, both in the manifest):

- **Winning ticket** (`piece-winning-ticket.html`) — a ticket
  face that states the win: the winner's name, the win line,
  and the **night stamp** — the date of the night of the win.
  Seats in the same hero slot as any ticket.
- **Text post** (`piece-text-post.html`) — content only, a
  statement and/or short lines. A text post is a first-class
  piece: whatever it is — a text post, the coin, or the ticket —
  it plugs into the same frame as the new situation requires.

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
- Coin sample (`formats/coin/daily-wire-coin.html`, FULL GOLD scheme,
  Wire face) rendered at exactly **1080 × 1080 px** and read in full:
  rim mark reads exactly LIVE WIRE TICKET™, insert reads exactly
  VICE CITY WIRE, with the mini sideways ticket, "THE BRIDGE DOESN'T
  CONNECT" and "No. 0002" on the face; nothing clipped; every color on
  the render traces to a `full-gold` scheme variable; no real coin's
  artwork appears anywhere in it.
- Format samples (all Daily Wire, `wire-pink-teal` scheme) rendered
  and read in full, Nov 22, 2026: poster **1275 × 1650 px** (Letter
  at 150 DPI), square **1080 × 1080 px**, vertical **1080 × 1920 px**,
  banner **1584 × 528 px**. Every render: masthead reads exactly
  THE DAILY WIRE, ticket face reads exactly LIVE WIRE TICKET™ ·
  VICE CITY WIRE, headline reads exactly "THE BRIDGE DOESN'T
  CONNECT", hero ticket sideways and in front, nothing clipped or
  overlapping.

- Completeness pass (Nov 22, 2026): the plug-in contract
  (`PLUG-IN.md`), the pieces manifest (`pieces/MANIFEST.md`), the
  text-post and winning-ticket pieces, and the coin-opener format
  were added. Coin-opener sample rendered at exactly
  **1080 × 1920 px** and read in full: marble scheme, reel slot
  labeled with the issue's reel, back line verbatim, footer
  correct. Regression renders after the naming pass (public
  pieces carry **Bumkus**, the LLC — never "Bumkus IP"): coin
  sample **1080 × 1080 px**, rim bottom mark reads exactly
  BUMKUS; newspaper sample **1275 × 1650 px** — dimensions
  unchanged. Static audits: all five schemes define the identical
  46-variable set; every variable the coin-opener frame reads is
  in that contract; zero hard-coded colors and zero inline styles
  in `pieces/`.

## Ownership

The newspaper template — both editions' frames, the ticket-slot frames,
the sideways hero treatment, the pieces system, the schemes, the format
boxes, and the coin (base and inserts) — is a design of the house. **© Bumkus · Licensed, never sold — see the
repository LICENSE.** The papers are ours: The Daily Wire is Vice City
Wire's newspaper; The Whited Daily is Garrett Whited's personal paper.

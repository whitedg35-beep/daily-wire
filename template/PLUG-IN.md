# PLUG-IN — The Contract

**The pieces just sit in and plug in.**

This file is the contract every frame, piece, and scheme in this
package honors. It exists so a new piece can be dropped into any
slot, on any surface, with **no frame edits** — and so the result
looks exactly like the house, every time.

## The three layers

Every finished surface in this system is three layers, in this
order:

1. **SURFACE** — the bottom, given. A newspaper page, a square,
   a vertical, a banner, a story, a feed slot — whatever the
   situation puts underneath. The surface is not ours to redesign;
   it is the ground the piece lands on.
2. **SCHEME MASK** — ours, applied. The schemes on file
   (`wire-pink-teal`, `full-gold`, `marble-gold-silver`,
   `whited-silver-brass`, `custom`) are masks: each one defines
   the same 46 CSS variables, and the frame reads only those
   variables. Lay a mask over a surface and everything on it
   reads as the house.
3. **PIECE** — the content, plugged in. A piece carries
   **content only**: text, a face, a name, a reel. It brings no
   styling, no color, and no dimensions of its own. It plugs in
   where it is needed, under the mask, on whatever surface is
   underneath.

**Surface-independence:** no matter what the bottom surface was,
we plug what we need where we need it, under those scheme masks.
The same piece, masked per surface, is the same piece everywhere.

## The FRAME-EXACTNESS RULE

**Plugging in a new piece changes ONLY the piece.**

Everything looks like it was before the plug-in: same frame,
same scheme, same trim, same motion grammar. The presentation
does not drift between pieces, between issues, or between
editions — and **the reels must represent the frame exactly**.
A reel built from this package carries the frame as specified
here: the sideways hero in front, the slot dimensions exact,
the back line verbatim. If a render disagrees with this file,
the render is wrong, not the frame.

Usage model, in one line: **the package is live as-is — to run a
new piece, plug it into the frame and replace the outer reel.
Nothing else moves.**

## Slot contracts

Dimensions are frame law. Pixel figures are at 150 DPI
(1in = 150px) unless the format is authored in pixels.

| Slot | Host frame(s) | Dimensions | Accepts (piece types) |
|---|---|---|---|
| Hero slot (sideways) | newspaper, poster, square, vertical, banner | newspaper 525×375px (3.5×2.5in); poster 945×675px; square 735×525px; vertical 920×657px; banner 588×420px — 7:5 always | hero ticket, **winning ticket** |
| Card slot (upright) | newspaper (left + right columns) | 375×525px (2.5×3.5in) | card slot |
| Headline zone | all frames | full width of the content box | headline |
| Article zones / bottom strip | newspaper, vertical | column width of the host grid | article, **text post** |
| Caption zone | newspaper, poster, square, vertical, coin | directly under its slot | caption, short text post |
| Coin insert zone | coin, coin-opener | Ø540px field inside the Ø726px rim (base Ø780px, canvas 1080×1080) | coin insert (wire / recipient / issue face) |
| Reel slot | coin-opener (B5, inside the square stage 1080×1080) | 984×984px | the outer reel (video) — replaceable, nothing else moves |
| Back line | coin-opener (B6), ticket backs | full width | fixed frame text — not a piece slot |

## Piece rules

A file belongs in `pieces/` only if all of these hold:

1. **Content only.** Text and structure in the frame's class
   hooks — nothing else. No inline styles, ever.
2. **No color.** A piece names no color, gradient, or image.
   All color reaches it through the frame CSS from the scheme's
   variables. (Verified across the package: zero hard-coded
   colors in `pieces/`.)
3. **No dimensions.** Size belongs to the slot, not the piece.
   The same piece seats at every scale its slot runs.
4. **Known hooks only.** A piece may use only the classes the
   frames style (`.piece-headline`, `.piece-article`,
   `.piece-caption`, `.piece-slot`, `.hero-ticket`,
   `.coin-insert`, and marker classes such as
   `.piece-text-post`, `.piece-winning-ticket`). If a piece
   needs a hook no frame styles, that is a template change —
   made once, in the frame, for every future piece.
5. **Drop-in test.** Paste the piece into its slot in any host
   frame, under any scheme, and it renders as the house with
   zero edits to the frame, the scheme, or the piece.

## The variable contract (frame ↔ scheme)

Pieces never touch variables; variables are the contract
between frames and schemes. Every scheme defines the same
46 variables — ink, paper, borders, banner, hero, slot,
caption, article — and every frame reads only those names.
A new scheme is valid when it defines all 46; a new frame is
valid when it reads no others. Slot dimensions are never
variables: size is frame law, not scheme taste.

One sanctioned exception: the `#ffffff` body backdrop in the
frame CSS sits **outside** the page box — it is the print/screen
canvas the box rests on, not a design surface, and no scheme
masks it.

## Piece types (all first-class)

| Piece type | File | What it carries |
|---|---|---|
| Headline | `pieces/piece-headline.html` | banner headline + standfirst |
| Article | `pieces/piece-article.html` | one story block |
| Caption | `pieces/piece-caption.html` | the one line under a slot |
| Card slot | `pieces/piece-card-slot.html` | the upright card's label + note |
| Hero ticket | `pieces/piece-hero-ticket.html` | the sideways ticket face |
| **Winning ticket** | `pieces/piece-winning-ticket.html` | a ticket face that states the win — winner's name, win line, night stamp |
| Coin insert | `pieces/piece-coin-insert.html` | the coin's face (wire / recipient / issue) |
| **Text post** | `pieces/piece-text-post.html` | a statement and/or short lines — content only, plugs into any text zone |
| Outer reel | (video file) | the reel that plays in the coin-opener's reel slot; the newspaper reels' moving content |

Any content type — **a text post, whatever it is, the coin, or
the ticket** — plugs into the same frame as the new piece. The
type changes; the plug-in doesn't.

## Formats covered by this contract

Newspaper (Letter) · Poster · Square · Vertical · Banner ·
Coin (base + insert) · **Coin-opener** (the seven-beat sequence:
wake → fall → roll → transform → face fall → pop to the square
→ back line; spec in `formats/coin-opener/`).

## Adding things

- **New piece:** write it to the piece rules, add it to
  `pieces/MANIFEST.md`, done. No frame edits.
- **New scheme:** copy `schemes/custom-scheme.css`, define all
  46 variables, done. No frame or piece edits.
- **New format:** a frame CSS + skeleton honoring this contract
  (marked drop zones, scheme variables only, slot dimensions
  stated here). A template change — made once, for every future
  issue.

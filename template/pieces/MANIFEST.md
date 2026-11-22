# Pieces Manifest

Every piece in this folder, its slot contract, and what swaps
per use. The contract itself lives in [`../PLUG-IN.md`](../PLUG-IN.md):
content only, no color, no dimensions, drop-in with no frame edits.

| Piece | File | Type | Drops into | Swap per use |
|---|---|---|---|---|
| Headline | `piece-headline.html` | text | Headline zone — all frames | headline + standfirst |
| Article | `piece-article.html` | text | Article zones, bottom strip (newspaper, vertical) | headline + paragraphs |
| Caption | `piece-caption.html` | text | Caption zone — under any slot | the one line |
| Text post | `piece-text-post.html` | text | Any text-bearing zone, any surface | statement + lines |
| Card slot | `piece-card-slot.html` | card | Card slot, upright 375×525px @150 DPI (newspaper columns) | label + note — never dimensions |
| Hero ticket | `piece-hero-ticket.html` | ticket | Hero slot, sideways, 7:5 (all formats) | headline, ticket number, meta |
| Winning ticket | `piece-winning-ticket.html` | ticket | Hero slot, sideways, 7:5 (all formats) | winner's name, win line, night stamp |
| Coin insert | `piece-coin-insert.html` | coin | Coin insert zone, Ø540px field (coin + coin-opener) | brand line, issue line, meta, mini-ticket line |

The **outer reel** (video) is the ninth piece: it has no file in
this folder — it seats in the coin-opener's reel slot
(984×984px, B5) and in the newspaper reels' motion build. Replace
the reel and nothing else moves (frame-exactness, PLUG-IN.md).

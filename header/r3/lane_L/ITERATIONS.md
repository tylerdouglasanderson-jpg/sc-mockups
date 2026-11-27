# I-007 lane L: header bar layout, type and logo (rounds 1-3)

2026-11-27. 42 variants (round 1: 20, round 2: 12, round 3: 10). Board in every mock: today's
`endgrain-bp.svg`. Files here: `gallery.html` (phone, top 3 first, then every round), `desktop.html`
(top 3 at 1280 web, 820 iPad upright, 1180 kitchen iPad), `build.py` + `variants_more.py` (the recipes),
`grades.json`, `contrast.json`, `fonts/` (IBM Plex Sans and EB Garamond, both OFL). Rebuild:
`python build.py shots`. Shots (scratch): `.../scratchpad/i007/shots_L/` (390 wide for every variant;
1280 / 820 / 1180 for the top 3).

Grades: Look, Fit, Brand, Ease, Standard (1-10, strict; self-grades run about 1 high). Contrast = cream
words against the lightest wood pixel behind them (99.5th percentile), shadows NOT counted.

## What I found before drawing (with lane R's RESEARCH.md)

- The signed-in app's bar is already one bar: 50 tall, wordmark Plex SemiBold Italic 22, saving cloud
  slot, 29 avatar. The drift is elsewhere: entry / welcome / setup / shopper link draw 44 or 58, and
  auth draws a 28 wordmark on the bar. "Same height everywhere" means fixing those, not the main bar.
- DESIGN 2.5.5 says no serif anywhere (Garamond was removed on purpose); 2.8.4 says no decorative
  shadows. Both shaped the picks.
- Fonts: only IBM Plex Sans (the app's) and EB Garamond were on this machine; downloads needed an
  approval I could not get. The other serif tries use Georgia and Palatino as stand-ins, named with their
  free twins (Gelasio, metric-compatible OFL; TeX Gyre Pagella). Slab serifs (Zilla Slab, Roboto Slab)
  were not tried: none was on disk.
- Today's board is safe for cream words: worst 5.37 to 5.5:1 behind any word.

## Round 1 (20 variants, wide spread)

| Id | Idea | Grades | Avg | Worst contrast | Verdict |
|---|---|---|---|---|---|
| L-r1-01 | Today's bar (control) | 6 8 5 7 6 | 6.4 | 5.48 | Name small and light on busy wood |
| L-r1-02 | 56 + SC tile 26 | 7 7 7 8 7 | 7.2 | 5.48 | Tile ties bar to app icon. Kept |
| L-r1-03 | 56, tile 28, Bold Italic 23 | 7 7 7 8 7 | 7.2 | 5.48 | 700 reads better than 600. Kept |
| L-r1-04 | Burned mark + Bold Italic 24 | 7 7 8 7 7 | 7.2 | 5.48 | On theme, can look like a hole. Kept |
| L-r1-05 | Bare cream "sc" glyph | 5 6 4 6 6 | 5.4 | 5.48 | Cut: reads as the name twice |
| L-r1-06 | Brass medallion | 6 5 6 7 6 | 6.0 | 5.48 | Cut: reads as a prize; gold off-palette |
| L-r1-07 | Calm dark patch, no mark | 6 7 6 7 6 | 6.4 | 8.17 | Patch drawn in the wrong place; fixed in r2 |
| L-r1-08 | Two weights in one word | 6 7 6 7 7 | 6.6 | 5.48 | Cut: difference too small to see |
| L-r1-09 | Condensed Plex 26 | 7 7 7 8 7 | 7.2 | 5.48 | Taller, stamped, app font. Kept |
| L-r1-10 | EB Garamond Italic 27 | 8 5 8 7 7 | 7.0 | 5.48 | Warm; breaks 2.5.5. Serif lane |
| L-r1-11 | Garamond upright Bold | 7 5 7 7 7 | 6.6 | 5.48 | Cut: book cover, not kitchen |
| L-r1-12 | Georgia Bold Italic (Gelasio) | 8 5 8 7 7 | 7.0 | 5.48 | Warm and sturdy. Serif lane |
| L-r1-13 | Palatino Bold (Pagella) | 6 5 6 7 7 | 6.2 | 5.48 | Cut: thin, bookish |
| L-r1-14 | Shadow + "Tyler" chip | 6 6 6 8 6 | 6.4 | 5.48 | Cut: heavy chip; decorative shadow |
| L-r1-15 | Search + quick add + bell | 5 4 5 6 6 | 5.2 | 5.48 | Cut: clutter; + doubles Capture; search ruled out (4.1.2) |
| L-r1-16 | Mark left, page name middle | 6 5 4 7 5 | 5.4 | 5.48 | Cut: repeats the page title; removed on purpose (D7 A) |
| L-r1-17 | 64 tall | 7 6 7 8 6 | 6.8 | 5.42 | Fine on a computer, costs phone height |
| L-r1-18 | 44 tall | 6 7 5 7 7 | 6.4 | 5.48 | Cramped; tile drops to 22 |
| L-r1-19 | Oil sheen + bottom edge | 7 7 7 8 7 | 7.2 | 5.77 | The edge makes it a real board. Kept |
| L-r1-20 | Household line under name | 6 6 6 7 6 | 6.2 | **4.40** | Cut: fails contrast; crowds the name |

Next: 56 tall, Bold 700, a mark at about cap height (28). Try three mark materials (cream tile,
burned, maple inlay), fix the patch, try a plank, keep the serif lane, test what the right side holds.

## Round 2 (12 variants)

| Id | Idea | Grades | Avg | Worst contrast | Verdict |
|---|---|---|---|---|---|
| L-r2-01 | Tile 28 + Bold Italic 24 + edge | 7 8 7 8 8 | 7.6 | 5.48 | Clean. Kept |
| L-r2-02 | Burned mark + edge | 7 7 8 7 8 | 7.4 | 5.48 | Dim at 28; refine |
| L-r2-03 | Maple inlay mark + edge | 7 8 8 7 8 | 7.6 | 5.48 | Calmer than cream, on theme. Kept |
| L-r2-04 | Tile + condensed 26 + edge | 7 8 7 8 8 | 7.6 | 5.48 | Kept |
| L-r2-05 | Calm patch (fixed) | 6 6 6 8 7 | 6.6 | 8.21 | Cut: hard edges, looks like a smudge |
| L-r2-06 | Long-grain plank holds the brand | 6 6 7 7 7 | 6.6 | 7.96 | Cut: looks like a big button |
| L-r2-07 | Avatar + chevron | 5 6 6 6 7 | 6.0 | 5.48 | Bug: avatar missing. Redone as r3-04 |
| L-r2-08 | Enamel badge + Georgia Bold Italic 23 | 8 5 8 8 8 | 7.4 | 5.48 | Best serif. Kept |
| L-r2-09 | Tile + Garamond Italic 28 | 7 5 8 7 8 | 7.0 | 5.48 | Cut: curly "ft", too fancy |
| L-r2-10 | Plex 650 at 94% width | 7 8 7 8 8 | 7.6 | 5.48 | Merged into r3-01 |
| L-r2-11 | 52 tall | 7 8 7 8 8 | 7.6 | 5.48 | Fallback height |
| L-r2-12 | Status slot lit (cloud + 4:12 timer) | 7 8 7 8 8 | 7.6 | 5.48 | Fits. Live status only, never buttons |

Next: lock 56 + Bold Italic 24; pick the mark; settle the edge (shadow vs a flat rule, because of
2.8.4); fix the chevron; refine the burn; one 52-tall twin.

## Round 3 (10 variants)

| Id | Idea | Grades | Avg | Worst contrast | Verdict |
|---|---|---|---|---|---|
| L-r3-01 | Tile + Bold Italic 24 + edge shadow + avatar 32 | 8 8 7 8 8 | 7.8 | 5.48 | Best Plex; shadow is the open question |
| L-r3-02 | Maple inlay + Bold Italic 24 | 7 8 8 7 8 | 7.6 | 5.48 | Tan mark and cream name fight a little |
| **L-r3-03** | Maple inlay + condensed Plex 650 26 | 7 8 8 8 8 | 7.8 | 5.48 | **Pick 2** |
| L-r3-04 | Avatar 30 + chevron | 7 7 7 8 8 | 7.4 | 5.48 | One more thing to read; most apps skip it |
| **L-r3-05** | Maple inlay + Georgia Bold Italic 23 (Gelasio) | 8 5 9 8 8 | 7.6 | 5.48 | **Pick 3** (needs a serif exception) |
| L-r3-06 | Oil sheen + edge + tile shadow | 7 7 8 8 7 | 7.4 | 5.77 | Cut: darker bottom; decorative shadow |
| L-r3-07 | r3-01 at 52 tall | 7 8 7 8 8 | 7.6 | 5.48 | Fallback height |
| L-r3-08 | Burned mark, shallower | 7 7 8 7 8 | 7.4 | 5.48 | Option if the cream tile feels too bright |
| L-r3-09 | r3-01 with status lit | 7 8 7 8 8 | 7.6 | 5.48 | Busiest state still fits at 390 |
| **L-r3-10** | r3-01 with a flat 1 px rule, no shadow | 8 9 7 8 8 | 8.0 | 5.48 | **Pick 1** |

Score trend (best avg per round): 7.2 → 7.6 → 8.0. Worst contrast of any kept variant: 5.48:1 (pass).
Only failure in 42: L-r1-20's household line, 4.40:1.

## Picks (the recipe for each, for the merge with lane A/B's board)

1. **L-r3-10.** Row 56 on every platform. SC tile (`favicon-tile.svg`) 28, gap 8, then "SupperCraft"
   IBM Plex Sans Bold Italic 24, letter spacing -1%. Right: status slot, then avatar 32 in a 44 target.
   Board ends in a 1 px `rgba(20,8,0,.55)` rule, no shadow.
2. **L-r3-03.** Same, but the mark is a light maple inlay (tan gradient, dark brown "sc", slight inset)
   and the name is Plex 650 Italic 26 at 88% width.
3. **L-r3-05.** Maple inlay + Georgia-style Bold Italic 23, shipped as Gelasio (OFL). Only with a logo
   exception to 2.5.5.

## What "the same everywhere" needs in code (for whoever builds it)

- One token `FRAME.headerRow` (56, or 50 if Tyler keeps it), read by every `Header` user. Remove the
  hard-coded 58s (`EntryParts.tsx` storyHeader, `SetupChrome.tsx`, `ShopParts.tsx` shopperHeader), the
  44 default (`h-hdr-landscape` in `Header.tsx`) and the unused `hdr-portrait`.
- The auth screens' 28 wordmark moves into the page; the bar always shows the 24 wordmark + mark.
- Wordmark size `scales.wordmark.header` 22 → 24, weight 600 → 700 (web and the native static face:
  `IBMPlexSans-BoldItalic` needs adding to the app.json font list).
- `AVATAR_SIZES.sm` stays 29 for rows; the header gets its own 32 (or keep 29: the difference is small).

## Still weak

- The cream tile is the brightest thing on the bar and the brand README calls the SC mark temporary.
- No slab serif tried, and the serif lane used stand-ins, not the real Gelasio / Pagella.
- Kitchen iPad from across the room: 24 is readable but not big; the kitchen at rest has no bar at all.
- Desktop: the wordmark sits at 28 from the edge, not exactly over the rail's labels (live code lines it up).
- All on today's board; lighter boards from lanes A/B need the contrast re-run (`python build.py shots`).

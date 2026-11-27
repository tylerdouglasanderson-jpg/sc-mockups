# I-007 lane A: the header board, refined (rounds 1-3)

Lane A stays close to today's board (`endgrain-bp.svg`) and tries to make it calmer, more real and easier to read.
43 boards in 3 rounds (14 + 12 + 17). Every tile file is kept in `tiles/`, including the cut ones.

- Make a tile: `python gen/board.py "<json params>" out.webp` (all knobs are in `DEFAULTS` in `gen/board.py`).
- Make and shoot a round: `python gen/shoot.py r3` (variants live in `gen/variants.py`). Shots go to the scratch folder.
- Rebuild the pages: `python gen/gallery.py`; score tables (bottom of this file): `python gen/tables.py`.
- Note: the generator changed between rounds (new ring drawing in round 2), so re-running round 1 now would draw
  slightly different r1 tiles. The kept r1 tiles are the ones that were graded.

## How each board was judged

- Every board was shown in the real bar, copied from the app: 50 px row (`FRAME.headerRow`), italic SemiBold
  "SupperCraft" at 22 px in header-text cream `#FAF4EB`, the 29 px avatar with its cream ring, cream page under it.
- Sizes shot: 1280x800 and 820x1180 (web: the tile repeats at its own size, as `TopInsetBoard` does), 390x844
  (iPhone: one image, cover, board under the 47 px status bar), 1180x820 (iPad: cover, 24 px inset), a 3x-wide tile
  strip to hunt seams, and a 2x zoom of the wordmark.
- Contrast: each page was shot again with the words hidden. "Words worst" = cream against the LIGHTEST pixel inside
  the wordmark's box (the hardest case, not an average). "Whole board worst" = cream against the lightest pixel
  anywhere on the board (matters if small cream words ever go elsewhere on the bar).
- Grades 1-10, strict: B beauty, E end-grain look, R easy to read, F fits the app, T tiles with no seam and small file.
  Anything with words under 4.5:1 got R5 at most.

## Round 1 (14 boards): spread out over the knobs

What it tried: block size 14-26, rings centred vs. curving from a heart off the block, glued strips of varying
width, species mix, calm vs. wide colour spread, glue darkness, per-block lustre, top light, bottom bevel, shadow,
and a quiet darker patch behind the wordmark.

What I saw:
- Today's look (bullseye rings, three flat colours) reads like clip art up close. Rings that curve from a heart
  outside the block (r1-02 onward) look far more like real end grain.
- Most round-1 boards FAIL contrast behind the words (4.3-4.5:1): the light blocks were too light. Only the calm and
  dark ones (r1-05, r1-08) and the ones with a top light or quiet patch (r1-10, r1-11) passed.
- Small blocks (14, 16) and dark wide glue (r1-14) look like bathroom tile or graph paper. Cut.
- Per-block lustre (r1-09) is invisible at 1x. Cut.
- Rings were thin and squiggly like fingerprints when zoomed.
- Wins: glued strips (r1-06), the species mix (r1-07), the bevel + shadow (r1-10), the quiet patch (r1-11), 24 px with
  an oil band (r1-13).

Cut: r1-01, 03, 04, 09, 12, 14 (r1-05 and r1-08 kept only as ideas: calm but flat and muddy).

Changes for round 2: new ring drawing (ring widths drift like good and lean years, rings a little oval, smoother
wobble, the heart side a touch darker, pores only in the light wood); the brightest wood capped at luminance 0.13;
softer glue (0.4, 0.6 px); bevel + page shadow + quiet patch as the standard overlay.

## Round 2 (12 boards): breed the winners

What I saw:
- Huge step up in looking like real wood. Every board now clears 4.5:1 behind the words (5.7-7.0:1).
- The honey colour turned olive once it was capped, and a negative hue nudge made grey-green blocks (r2-02, 05, 08).
- Columns that keep one tone all the way down make vertical stripes on the phone (r2-12).
- The quiet patch at 0.3 shows as a dark blob on the left in some (r2-01, r2-05).
- The bevel's light lip reads as a separate light strip on the phone.
- Best: r2-04 (24 px strips + oil band) and r2-10 (wide soft rings), both 40/50.

Cut: r2-02, 05, 07, 08 (olive, busy, grid-like); r2-09 (no patch: readable but plain).

Changes for round 3: cap 0.12; smaller hue nudge; columns hold their tone less (strip_hold 0.45); a wider, softer
quiet patch (0.24, 200x40); amber in place of honey; a slim 4 px dark edge with no light lip tried as an option.

## Round 3 (17 boards): refine, then fix the bottom edge, then make a day set

What I saw:
- r3-01, 03, 04 and 08 all solid (40/50). The slim edge without the lip (r3-08) is cleaner than the lip.
- New problem spotted: with 22 or 24 px blocks the 50 px web bar ends in a thin sliver of a third row just above the
  edge. It looks untidy. 25 px blocks give exactly two whole rows on web (r3-12, 13, 14): the tidiest bars so far.
- The day sets (r3-15, 16, 17 from the r3-13 recipe; r3-09, 10, 11 from r3-03) read as one family, each day a
  little different, as DESIGN.md 4.1.1 asks.
- Seams: none visible in any 3x strip or at 1280 / 820 (every mark stays inside its own block, and the block grid
  fills the tile exactly).
- Files: 25-31 KB WebP each at 2x, against 300 KB for today's SVG.

### Top 3

1. **A-r3-13** (42/50: B9 E8 R8 F9 T8). Calmest and most finished: 25 px glued strips, warm colours, soft oil band,
   slim dark edge, two whole rows on web. Words 7.0:1 at worst.
2. **A-r3-14** (42/50: B8 E9 R8 F9 T8). Most "cutting board": amber and walnut blocks, each darker on its heart side.
   Livelier, still 6.4:1 behind the words.
3. **A-r3-12** (41/50: B8 E8 R8 F9 T8). Wide soft rings, light oil band; the middle road.

Day set to ship (if r3-13 wins): r3-13, r3-15, r3-16, r3-17.

Score trend (best sum per round): r1 38 -> r2 40 -> r3 42.

## Still weak (for the next rounds or the merge with lane L)

- iPad native: the app draws the board with expo-image "cover", so on a 1180 wide iPad the tile is blown up about
  1.6x (blocks look ~40 px). True for every board, today's too. Fix: tile it on native as well (RN Image
  `resizeMode="repeat"`), or ship a wider tile for iPad. A code change, not a texture change.
- The bevel, page shadow, oil band and quiet patch are CSS layers in the mock. In the app each needs one extra
  absolute view in `TopInsetBoard` (a gradient view or a tiny PNG strip). The tile alone still looks good without
  them, but the quiet patch is what lifts the words from ~5.7 to ~7:1.
- The quiet patch is placed for the current wordmark spot; if lane L moves the logo or adds the SC mark, the patch
  moves with it.
- "Whole board worst" is 4.45-4.9 on the picks: one or two of the brightest pixels sit in the oil band. Fine for the
  wordmark (7:1), but if small cream words ever go elsewhere on the bar, drop the oil band to ~0.12.
- 25 px blocks give two whole rows only at today's 50 px height. If lane L changes the height, pick the block size so
  the bar holds whole rows (height / 2 or height / 3).
- Self-grades only; no outside panel has graded these yet.

## Score tables

### r1 table

| id | what it tries | B | E | R | F | T | sum | words worst (1280 / 820 / iPhone / iPad) | whole board worst | KB |
|---|---|---|---|---|---|---|---|---|---|---|
| A-r1-01 | today's board redrawn: same 18 px blocks and 3 colours, rings near the middle | 6 | 7 | 5 | 8 | 7 | 33 | 4.4 / 4.4 / 4.5 / 4.5 | 3.97 | 45 |
| A-r1-02 | rings from a heart off the block, so they curve like real end grain | 6 | 7 | 5 | 8 | 8 | 34 | 4.3 / 4.3 / 4.5 / 5.0 | 4.28 | 34 |
| A-r1-03 | small 14 px blocks, tight colours, fine rings | 5 | 6 | 5 | 8 | 7 | 31 | 4.5 / 4.5 / 4.8 / 4.9 | 4.25 | 40 |
| A-r1-04 | 22 px blocks, wider colour spread, softer glue | 6 | 7 | 5 | 8 | 8 | 34 | 4.3 / 4.3 / 4.5 / 4.4 | 4.31 | 38 |
| A-r1-05 | big 26 px blocks, calm | 6 | 6 | 7 | 7 | 8 | 34 | 5.7 / 5.7 / 5.5 / 6.2 | 4.97 | 27 |
| A-r1-06 | real glued strips: column widths vary, odd rows mirrored | 7 | 8 | 5 | 8 | 8 | 36 | 4.4 / 4.4 / 4.6 / 4.6 | 4.35 | 36 |
| A-r1-07 | species mix: walnut, cherry and honey blocks | 7 | 8 | 6 | 8 | 8 | 37 | 4.7 / 4.7 / 4.5 / 5.2 | 4.02 | 33 |
| A-r1-08 | very calm: tight colours, low soft rings, light glue | 6 | 6 | 7 | 8 | 8 | 35 | 5.7 / 5.7 / 6.2 / 6.7 | 5.66 | 19 |
| A-r1-09 | each block oiled: soft lustre and a tiny chamfer | 6 | 7 | 5 | 8 | 8 | 34 | 4.4 / 4.4 / 4.5 / 5.5 | 4.21 | 38 |
| A-r1-10 | warm top light, bottom bevel and a shadow on the page | 7 | 7 | 7 | 8 | 8 | 37 | 5.3 / 5.3 / 4.9 / 5.4 | 4.22 | 34 |
| A-r1-11 | a quiet darker patch behind the wordmark, plus a bevel | 7 | 7 | 8 | 8 | 8 | 38 | 6.3 / 6.3 / 6.9 / 6.6 | 4.18 | 35 |
| A-r1-12 | 16 px blocks, crisp dense rings, faint ray flecks | 5 | 6 | 5 | 7 | 6 | 29 | 4.5 / 4.5 / 4.6 / 5.0 | 4.12 | 63 |
| A-r1-13 | 24 px glued strips with an oil sheen band | 7 | 7 | 6 | 7 | 8 | 35 | 4.7 / 4.7 / 4.6 / 5.0 | 3.90 | 35 |
| A-r1-14 | crisp grid: dark wide glue lines | 5 | 6 | 5 | 8 | 7 | 31 | 4.5 / 4.5 / 4.5 / 4.7 | 4.11 | 39 |

### r2 table

| id | what it tries | B | E | R | F | T | sum | words worst (1280 / 820 / iPhone / iPad) | whole board worst | KB |
|---|---|---|---|---|---|---|---|---|---|---|
| A-r2-01 | from r1-06: 20 px glued strips, today colours, new rings, bevel + quiet patch | 7 | 8 | 7 | 8 | 8 | 38 | 6.8 / 6.8 / 6.9 / 6.7 | 4.35 | 30 |
| A-r2-02 | from r1-07: species mix toned down, 20 px strips | 6 | 7 | 7 | 8 | 8 | 36 | 6.2 / 6.2 / 6.9 / 6.3 | 4.26 | 31 |
| A-r2-03 | from r1-11: even 18 px grid, warm colours, stronger quiet patch | 7 | 7 | 8 | 8 | 8 | 38 | 7.0 / 7.0 / 7.3 / 7.0 | 4.53 | 29 |
| A-r2-04 | from r1-13: 24 px strips with an oil sheen band | 8 | 8 | 8 | 8 | 8 | 40 | 6.3 / 6.3 / 6.5 / 6.9 | 4.08 | 26 |
| A-r2-05 | 22 px species mix with a warm top light | 6 | 7 | 7 | 8 | 8 | 36 | 5.9 / 5.9 / 6.5 / 7.0 | 4.25 | 27 |
| A-r2-06 | from r1-08: calm, a bit more colour so it is not muddy | 7 | 7 | 8 | 8 | 8 | 38 | 7.0 / 7.0 / 6.8 / 6.6 | 4.88 | 24 |
| A-r2-07 | 20 px, firmer glue lines (not graph paper) | 6 | 7 | 7 | 8 | 8 | 36 | 6.5 / 6.5 / 6.3 / 6.9 | 4.45 | 32 |
| A-r2-08 | 18 px strips, species mix, tiny chamfer per block | 6 | 7 | 7 | 8 | 7 | 35 | 6.2 / 6.2 / 6.4 / 6.5 | 4.40 | 31 |
| A-r2-09 | no quiet patch: a darker board (cap 0.115) does the job alone | 7 | 7 | 7 | 8 | 8 | 37 | 5.7 / 5.7 / 5.9 / 6.1 | 5.06 | 26 |
| A-r2-10 | 20 px, wider soft rings | 8 | 8 | 8 | 8 | 8 | 40 | 6.6 / 6.6 / 6.5 / 6.7 | 4.81 | 26 |
| A-r2-11 | 24 px species mix, strong heart side, faint top light | 7 | 8 | 8 | 8 | 8 | 39 | 6.8 / 6.8 / 6.6 / 7.0 | 4.41 | 28 |
| A-r2-12 | deeper oiled walnut colours, light quiet patch | 7 | 8 | 7 | 8 | 8 | 38 | 5.7 / 5.7 / 6.1 / 6.2 | 4.47 | 29 |

### r3 table

| id | what it tries | B | E | R | F | T | sum | words worst (1280 / 820 / iPhone / iPad) | whole board worst | KB |
|---|---|---|---|---|---|---|---|---|---|---|
| A-r3-01 | r2-04 refined: 24 px strips, oil band, softer quiet patch | 8 | 8 | 8 | 8 | 8 | 40 | 6.6 / 6.6 / 6.7 / 6.7 | 4.47 | 27 |
| A-r3-02 | r2-10 refined: 20 px, wide soft rings | 7 | 8 | 8 | 8 | 8 | 39 | 6.7 / 6.7 / 6.6 / 7.6 | 4.83 | 27 |
| A-r3-03 | r2-04 x r2-10: 22 px strips, wide soft rings, light oil band | 8 | 8 | 8 | 8 | 8 | 40 | 7.3 / 7.3 / 7.6 / 7.3 | 4.45 | 25 |
| A-r3-04 | r2-11 refined: 24 px, amber in place of honey, strong heart side | 8 | 8 | 8 | 8 | 8 | 40 | 7.0 / 7.0 / 6.7 / 6.6 | 4.66 | 29 |
| A-r3-05 | r2-12 refined: deep walnut, columns hold their tone less | 7 | 8 | 8 | 8 | 8 | 39 | 7.0 / 7.0 / 6.3 / 7.8 | 4.95 | 28 |
| A-r3-06 | r2-01 refined: today's three colours, 20 px strips | 7 | 7 | 8 | 8 | 8 | 38 | 7.1 / 7.1 / 6.6 / 7.5 | 4.55 | 31 |
| A-r3-07 | r2-06 refined: calm, rings a little clearer, 22 px | 7 | 7 | 8 | 8 | 8 | 38 | 6.7 / 6.7 / 6.7 / 7.5 | 5.11 | 25 |
| A-r3-08 | r3-03 with a slim dark edge and no light lip | 8 | 8 | 8 | 8 | 8 | 40 | 7.3 / 7.3 / 7.6 / 7.3 | 4.95 | 25 |
| A-r3-09 | day 2 of the r3-03 recipe (new seed) | 7 | 8 | 8 | 8 | 8 | 39 | 6.3 / 6.3 / 7.4 / 6.7 | 4.67 | 25 |
| A-r3-10 | day 3 of the r3-03 recipe (new seed) | 8 | 8 | 8 | 8 | 8 | 40 | 6.9 / 6.9 / 7.0 / 7.2 | 4.41 | 26 |
| A-r3-11 | day 4 of the r3-03 recipe (new seed) | 8 | 8 | 8 | 8 | 8 | 40 | 6.6 / 6.6 / 6.7 / 6.6 | 4.61 | 26 |
| A-r3-12 | r3-08 with 25 px blocks: exactly two whole rows in the 50 px bar | 8 | 8 | 8 | 9 | 8 | 41 | 6.6 / 6.6 / 6.8 / 7.4 | 4.98 | 26 |
| A-r3-13 | r3-01 (oil band) with 25 px blocks and the slim edge | 9 | 8 | 8 | 9 | 8 | 42 | 7.0 / 7.0 / 7.6 / 7.1 | 4.87 | 29 |
| A-r3-14 | r3-04 (amber, heart side) with 25 px blocks and the slim edge | 8 | 9 | 8 | 9 | 8 | 42 | 6.5 / 6.5 / 6.4 / 6.7 | 4.90 | 31 |
| A-r3-15 | day 2 of the r3-13 recipe (new seed) | 8 | 8 | 8 | 9 | 8 | 41 | 7.0 / 7.0 / 6.7 / 6.9 | 4.45 | 29 |
| A-r3-16 | day 3 of the r3-13 recipe (new seed) | 8 | 8 | 8 | 9 | 8 | 41 | 6.6 / 6.6 / 7.4 / 6.7 | 4.68 | 29 |
| A-r3-17 | day 4 of the r3-13 recipe (new seed) | 8 | 8 | 8 | 9 | 8 | 41 | 6.5 / 6.5 / 6.7 / 6.6 | 4.61 | 29 |

# I-007 lane M (merge): the header bar, rounds 4-6

2026-11-27. 33 boards in 3 rounds (round 4: 14, round 5: 10, round 6: 6 finals + 3 day-set boards), all in ONE
shared bar. Plus: every page kind, narrow phones (320-393) with a lit timer and saving cloud, native vs web, and the
SC mark side by side.

Files: `gallery.html` (phone; top 3 first, day set, every round, then the page / narrow / native / mark sheets),
`desktop.html` (top 3 at 1280, 820, 1180 and 2560), `tiles/` (every board, `<id>@2x.webp` + `<id>@3x.webp`),
`results.json` (tile stats + contrast per width), `pages_check.json` (page sheets: contrast + narrow-phone rule).
Recipes: `gen/board_m.py` (generator), `gen/variants.py` + `variants_r5.py` + `variants_r6.py`, `gen/mock.py` (the one
bar), `gen/shoot.py r4|r5|r6` (tiles, shots, contrast, sheets), `gen/build_pages.py shots`, `gen/grades.py`,
`gen/tables.py` (fills the tables below). Shots: scratch `.../scratchpad/i007/shots_M/`.

## The one bar (every board, every page)

- Lane L's L-r3-10 with the panel fixes: row **56**, SC mark (warm cream tile **26**, gap 8), "SupperCraft" IBM Plex Sans
  Bold Italic 24 (-1%), account avatar **29** in a 44 target top right, status slot (saving cloud, timer) left of it.
- Board ends in a **flat 1 px rule** `rgba(20,8,0,.55)`. No drop shadow, no quiet patch, no oil or overlay layer.
- Phone: status bar 47 above the row (also tested 20, 24, 50, 59). iPad: 24. Web: none.

## The tile (what the code must use)

- Every board is **one tile, 1440 x 140 CSS px** = 5 whole rows of **28 px**. Files: `@2x` 2880x280, `@3x` 4320x420 WebP.
- CSS: `background-size: 1440px 140px; background-position: left bottom; background-repeat: repeat`. Anchored to the
  BOTTOM, so the 56 row always shows exactly two whole rows, whatever the status bar is above it.
- 1440 wide: no repeat at all up to 1440; at 2560 it repeats once (I could not spot it at 1x, see "still weak").
- Weight: about 85-94 KB per board for 2x + 3x (r6-06: 77 KB). One board: 90 KB. Day set of 3: 274 KB. Day set of 4:
  367 KB at these settings, **over the 350 budget**; it fits at WebP quality 46/36 (measured 342 KB).
- Native (a build item, not done here): `TopInsetBoard` draws an RN `Image` with `resizeMode="repeat"`, absolute, left 0,
  right 0, bottom 0, height 140 (a multiple of 140 if a bar is ever taller), instead of expo-image `cover`; ship
  `board.webp` / `board@2x.webp` / `board@3x.webp` so iOS picks its scale. Web: `webTileStyle` gets
  `backgroundSize: '1440px 140px'` and `backgroundPosition: 'left bottom'` (today `720px 108px`, top-anchored).
  The gallery shows what "cover" does to this tile today: blocks ~27 px on a 390 phone and ~30 px on a 1180 iPad
  instead of 36.

## How it was judged

- Grades 1-10, strict (self-grades run about 1 high): **B**eauty, **E**thos (clearly warm end grain, the house family),
  **R**eadability, **F**it (rows whole, header brown family, nothing off-palette), **T**iling + weight.
- Contrast: each width was shot again with the name, mark, avatar and icons hidden; the number is cream `#FAF4EB`
  against the **single lightest pixel** in the box of the name, the mark and the account (avatar + ring), at 390 (3x
  render), 820, 1180, 1280 (2x). Gate 4.5, aim 5. "Whole bar worst" = lightest pixel anywhere in the 56 row.
- "Near-equal neighbours" = pairs of touching blocks whose mean lightness differs by under 1.5 L* (what makes planks
  and clumps). Lower is better.
- Looked at every round as contact sheets at 390 (2x) and at 1280 (true 1x), plus 2x zooms and the 3x tile at 1:1.

## What changed in the generator (vs lanes A and B)

- Blocks drawn one by one, nothing crosses a glue line (lane A's method), so the tile wraps with no seam both ways.
- Rings: wider (3.6-4.6 px), darker latewood, strength drawn per block (0.12-0.30); most blocks show arcs from a heart
  off the block; about **1 in 4** holds its own heart (off-centre from round 5, so no stamped targets).
- Tone: picked per block so no block is near-equal to its left, upper or upper-left neighbour, and no jump is huge
  (no planks, no checker). Colour from a warm ramp: A-r3-14's spread with the lightest and darkest pulled a third in;
  hue clamped 20-33 degrees and saturation 0.66-0.86, so no grey, olive or mauve block is possible.
- Light: optional, baked into the tile and y-only (repeats cleanly). Luminance soft-capped in linear light (keeps hue).

## Round 4 (14 boards): breed A-r3-14, A-r3-12/13, B-r3-03 into the one bar

What I saw:
- Rings now read at 1x (lane A's main fault fixed). Every board passes: worst 5.1-6.0:1.
- 28 px boards are a bit busy at 1x; 32 and 36 px blocks read calmer.
- Too many bullseye hearts on the B-style boards (r4-08, 09): the "thumbprint" problem in a new form.
- Baked oil band, top light and baked edge (r4-02, 07, 14): not visible at a strength that keeps contrast. Cut.
- Calmer tones (r4-04) doubled the near-equal neighbours: muddy. Cut.
- Files ~125 KB per board (2x+3x): too heavy for a day set.
Best: **M-r4-12** (warm 32 px glued strips), 38/50.

Changes for round 5: hearts off-centre (0.15-0.4 of a block), thinner latewood, wider spread of ring strength, bigger
min tone gap, stronger warm tints, no fibre noise, WebP 50/42 (files ~85 KB).

## Round 5 (10 boards)

What I saw:
- Fewer targets; the wood is more real. Amber on 36 px strips (r5-04) is calmest: only 25 near-equal pairs of 360.
- House colours (r5-05) lean honey/olive at 1x: cut. Wide soft rings look blurry (r5-06); flat warm 28 (r5-07): cut.
- New fault: heart blocks went dark and muddy (rings faded near the heart, plus heart-side darkening twice).
Best: **M-r5-04**, 40/50.

Changes for round 6: heart blocks get full-strength rings and less heart-side darkening.

## Round 6 (6 finals + day set)

What I saw:
- The heart fix works: every block has clear rings; no muddy blocks. r6-01 is the most "oiled cutting board" yet.
- r6-05: a baked oil band at 0.10 still barely shows and costs whole-bar contrast (5.1). Baked light is not worth it.
- r6-04 (warm rich 32): reddish, 66 near-equal pairs, 5.5: cut. r6-02's richer tints make a few orange-red blocks.
- Day set r6-01, 07, 08, 09 reads as one family; r6-08 has a lighter block under the mark (5.4, still passes).

Score trend (best per round): r3 (panel) 7/10 per lens → r4 38 → r5 40 → r6 41 (self, /50).

## Top 3

1. **M-r6-01** (41: B8 E9 R8 F8 T8). Amber and walnut tints on 36 px glued strips, clear rings in every block, 1 in 4
   with its heart, calm behind the name. Worst contrast **6.01:1**. 33 + 57 KB.
2. **M-r6-03** (40: B8 E8 R8 F8 T8). Same wood on 32 px blocks with firmer glue: more "butcher block", busier at 1x.
   Worst **6.21:1**. 36 + 60 KB.
3. **M-r6-06** (41: B7 E8 R9 F8 T9). Pick 1 with quieter rings: calmest behind the words, lightest files (29 + 48 KB);
   the safe one for the kitchen iPad far away. Worst **6.06:1**.

Day set (if Tyler wants the board to vary by day): r6-01, r6-07, r6-08, r6-09 (4 boards: re-encode at 46/36 to fit 350
KB, or ship 3).

## Every page, the narrow phones, the mark (on pick 1)

- Signed in, welcome/setup, Cook option B: name 6.3, mark 6.5, account 6.38. Kitchen iPad at 1180: 7.0+.
- Sign-in (signed out): **nothing top right** (the page IS the account step); the big 28 wordmark moves into the page.
  Other signed-out pages (sign-up): a plain "Sign in" word where the account sits (6.38:1).
- Shopper link: "Shared list" where the account sits (6.25:1). Same 56 bar (today 58).
- Cook: shown both ways. A (today, research pick): no board, tan band. B: the one bar on top (timer slot useful).
  Kitchen iPad at rest: shown with the bar. Both are questions for Tyler, not assumed.
- Narrow phones, saving cloud + timer lit, rule "timer drops its numbers first, then the cloud folds into a gold dot
  on the account; mark and name never change" (measured room between name and right side, need 12):
  320: both steps, 43 px · 360: timer to icon, 39 px · 375: 4:12 fits (25 px), 1:04:12 timer to icon (54 px) ·
  390: fits (40 px; 1:04:12 17 px) · 393 (status 59): fits (43 px; 1:04:12 20 px). Nothing collides.
  Rows stay whole at the bar's bottom under status bars 20, 24, 47, 50, 59.
- SC mark: warm cream 26 lets the name be seen first; bright cream 28 still pulls the eye; maple 26 is calmer still but
  drifts from the app icon; no mark is clean but loses the icon tie. Pick: **warm cream 26**, loaded from one file
  (the brand README calls the mark temporary). Mark contrast against the wood: 6.5.

## Still weak

- Self-grades only. No outside panel has seen rounds 4-6; expect about 1 point lower per lens.
- At 2560 the 1440 tile repeats once. I could not spot it at 1x (no standout block), but a careful eye matching blocks can.
- A 4-board day set at full quality is 367 KB (over 350). Ship 3, or re-encode at 46/36 (342 KB, not re-graded).
- The warm mark tile is a new colour (`#EFDDBE` inside the favicon tile); if Tyler wants the bar to match the home-screen
  icon exactly, the icon changes too, or keep the bright cream at 26.
- Wordmark 24 / 700 and the 56 row still change written rules (DESIGN 2.5.6 says 22; FRAME.headerRow is 50): Tyler's OK.
- Native tiling is only mocked in the browser; it must be checked on a device after the code change.
- No dark mode: the header has no dark palette entry.

## Score tables

<!-- TABLES -->
### Round 4 table

| id | from | what it tries | B | E | R | F | T | sum | worst contrast 390 / 820 / 1180 / 1280 | whole bar worst | near-equal neighbours | KB 2x+3x | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| M-r4-01 | A-r3-14 | A-r3-14 on 28 px rows: amber + walnut tints, darker heart side, trimmed spread | 7 | 8 | 8 | 8 | 6 | 37 | 5.92 / 5.73 / 5.73 / 5.73 | 5.24 | 61/459 | 46+80 | keep: Lively and clearly wood at 1x; a few very dark blocks; 125 KB for 2x+3x. |
| M-r4-02 | A-r3-14 | r4-01 + a soft oil band baked into the tile, above the name | 7 | 8 | 8 | 8 | 6 | 37 | 5.92 / 5.59 / 5.59 / 5.59 | 5.24 | 64/459 | 46+80 | cut: The baked oil band is too faint to see; stronger would cost contrast. |
| M-r4-03 | A-r3-14 | r4-01 with wider, softer rings | 7 | 7 | 8 | 8 | 7 | 37 | 6.04 / 5.73 / 5.73 / 5.73 | 5.73 | 57/459 | 40+69 | keep: Wider, softer rings; a little blurry. |
| M-r4-04 | A-r3-14 | r4-01, calmer: tones trimmed further (0.8) | 6 | 7 | 8 | 8 | 6 | 35 | 6.38 / 6.13 / 6.13 / 6.04 | 5.72 | 116/459 | 46+80 | cut: Calmer tones doubled the near-equal neighbours (116 pairs): muddy patches. |
| M-r4-05 | A-r3-13 | A-r3-13 recipe on 28 px rows: warm, oil band + slim edge baked in | 7 | 8 | 8 | 8 | 6 | 37 | 6.13 / 5.76 / 6.28 / 5.63 | 5.17 | 98/459 | 45+80 | keep: Warm and reddish; many near-equal neighbours (98). |
| M-r4-06 | A-r3-12 | A-r3-12 recipe: wide soft rings, calm | 7 | 7 | 8 | 8 | 7 | 37 | 6.25 / 6.03 / 6.23 / 6.03 | 5.86 | 92/459 | 36+61 | keep: Calm and plain. |
| M-r4-07 | A-r3-13 | r4-05 + a soft top light under the status bar (phone/iPad only) | 6 | 7 | 8 | 8 | 6 | 35 | 6.08 / 5.92 / 5.97 / 5.57 | 4.99 | 103/459 | 46+81 | cut: The top light does not show; worst contrast falls to 5.6. |
| M-r4-08 | B-r3-03 | B-r3-03 recipe: 36x28 blocks, house colours, 1 in 3 with its heart | 7 | 7 | 8 | 8 | 6 | 36 | 5.79 / 5.70 / 5.70 / 5.70 | 5.06 | 64/360 | 46+79 | keep: The B shape (36x28) works, but too many bullseye hearts. |
| M-r4-09 | B-r3-03 | r4-08 as glued strips (widths vary) | 6 | 7 | 7 | 8 | 6 | 34 | 5.82 / 5.14 / 5.14 / 5.14 | 5.14 | 62/360 | 44+80 | cut: Strips put a light patch right behind the name (5.1). |
| M-r4-10 | B-r3-03 | r4-08, 1 in 4 hearts, softer rings | 7 | 7 | 8 | 8 | 7 | 37 | 5.68 / 5.55 / 5.60 / 5.60 | 4.89 | 52/360 | 41+72 | keep: Softer B board; still a few targets. |
| M-r4-11 | A-r3-14 x B-r3-03 | amber colours on 36 px blocks | 7 | 8 | 8 | 8 | 6 | 37 | 6.03 / 6.02 / 5.91 / 5.91 | 5.64 | 54/360 | 42+75 | keep: Amber colours on 36 px blocks: calm, warm. |
| M-r4-12 | A-r3-13 x B-r3-03 | warm colours on 32 px glued strips | 8 | 8 | 8 | 8 | 6 | 38 | 5.74 / 5.74 / 5.74 / 5.74 | 5.63 | 73/405 | 45+80 | keep: Best of round 4: warm 32 px glued strips, calm behind the name. |
| M-r4-13 | A-r3-14 | r4-01 with firmer glue lines (a crisper board) | 7 | 8 | 8 | 8 | 6 | 37 | 6.08 / 6.03 / 5.57 / 6.03 | 5.51 | 51/459 | 46+82 | keep: Firmer glue reads as a crisper board (idea kept). |
| M-r4-14 | A-r3-14 | r4-01 + oil band + slim baked edge (the full board object) | 7 | 8 | 8 | 8 | 6 | 37 | 6.16 / 5.44 / 6.23 / 5.99 | 5.22 | 47/459 | 45+80 | cut: The baked edge is lost next to the 1 px rule; oil band unseen. |

### Round 5 table

| id | from | what it tries | B | E | R | F | T | sum | worst contrast 390 / 820 / 1180 / 1280 | whole bar worst | near-equal neighbours | KB 2x+3x | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| M-r5-01 | M-r4-12 | r4-12 refined: warm 32 px glued strips, hearts off-centre, thinner rings | 7 | 8 | 8 | 8 | 8 | 39 | 6.05 / 5.95 / 5.95 / 5.95 | 5.69 | 57/405 | 32+55 | keep: r4-12 refined; fewer targets; 88 KB. |
| M-r5-02 | M-r4-12 x M-r4-01 | r5-01 shape in the amber colours of A-r3-14 | 7 | 8 | 8 | 8 | 8 | 39 | 6.38 / 5.99 / 6.38 / 6.38 | 5.53 | 45/405 | 33+56 | keep: Amber 32: lively, warm. |
| M-r5-03 | M-r4-01 | r4-01 refined: amber, 28 px strips | 7 | 8 | 8 | 8 | 8 | 39 | 6.33 / 6.03 / 6.03 / 6.03 | 5.35 | 42/459 | 34+57 | cut: 28 px blocks get busy at 1x next to 32 and 36. |
| M-r5-04 | M-r4-11 | r4-11 refined: amber on 36 px glued strips | 8 | 8 | 8 | 8 | 8 | 40 | 6.51 / 6.10 / 6.10 / 6.10 | 6.02 | 25/360 | 31+54 | keep: Best of round 5: amber on 36 px strips, fewest near-equal neighbours (25). |
| M-r5-05 | M-r4-10 | r4-10 refined: house colours, 36 px, soft rings | 6 | 7 | 8 | 7 | 8 | 36 | 6.09 / 5.70 / 5.90 / 5.90 | 5.30 | 32/360 | 31+51 | cut: House colours lean honey/olive at 1x. |
| M-r5-06 | M-r4-03 | r4-03 refined: amber 28, wide soft rings | 7 | 7 | 8 | 8 | 8 | 38 | 5.99 / 6.01 / 6.01 / 6.01 | 5.14 | 43/459 | 30+48 | cut: Wide soft rings look blurry. |
| M-r5-07 | M-r4-06 | r4-06 refined: warm 28, wide soft rings | 6 | 7 | 8 | 8 | 8 | 37 | 5.66 / 5.86 / 5.86 / 6.03 | 5.66 | 78/459 | 27+44 | cut: Flat; 78 near-equal pairs. |
| M-r5-08 | M-r5-01 | r5-01 with richer cherry + amber tints | 8 | 8 | 8 | 7 | 8 | 39 | 5.93 / 6.04 / 6.04 / 5.94 | 5.18 | 62/405 | 33+56 | keep: Richer cherry tints, but a few blocks go orange. |
| M-r5-09 | M-r5-01 | r5-01 with ring widths that vary more (good and lean years) | 7 | 8 | 8 | 8 | 8 | 39 | 6.30 / 6.23 / 6.23 / 6.23 | 5.57 | 62/405 | 32+54 | cut: Ring widths vary more, no clear gain. |
| M-r5-10 | M-r5-02 | r5-02 with firmer glue lines | 7 | 8 | 8 | 8 | 8 | 39 | 6.47 / 6.25 / 6.25 / 6.47 | 5.24 | 41/405 | 34+58 | keep: Firmer glue on amber 32. |

### Round 6 table

| id | from | what it tries | B | E | R | F | T | sum | worst contrast 390 / 820 / 1180 / 1280 | whole bar worst | near-equal neighbours | KB 2x+3x | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| M-r6-01 | M-r5-04 | r5-04 refined: amber on 36 px glued strips, clear heart blocks | 8 | 9 | 8 | 8 | 8 | 41 | 6.31 / 6.01 / 6.30 / 6.26 | 5.63 | 32/360 | 34+57 | top: Most like a real oiled board: amber and walnut tints on 36 px glued strips, clear rings in every block, calm behind the name. |
| M-r6-02 | M-r5-04 x M-r5-08 | r6-01 with richer cherry + amber tints | 8 | 8 | 8 | 7 | 8 | 39 | 6.55 / 6.13 / 6.45 / 5.99 | 5.69 | 32/360 | 34+57 | keep: Richer tints; a few orange-red blocks stand out at 1280. |
| M-r6-03 | M-r5-10 | r5-10 refined: amber 32 px strips, firmer glue | 8 | 8 | 8 | 8 | 8 | 40 | 6.44 / 6.21 / 6.44 / 6.45 | 5.55 | 36/405 | 36+60 | top: Same wood on smaller 32 px blocks with firmer glue: more "butcher block", a bit busier at 1x. |
| M-r6-04 | M-r5-08 | r5-08 refined: warm 32 px strips, rich tints | 7 | 8 | 8 | 7 | 8 | 38 | 5.75 / 5.52 / 5.52 / 5.52 | 5.52 | 66/405 | 35+58 | cut: Reddish, 66 near-equal pairs, worst contrast 5.5. |
| M-r6-05 | M-r6-01 | r6-01 + a soft oil band baked in across the top of the bar | 7 | 9 | 8 | 8 | 8 | 40 | 6.38 / 6.00 / 6.38 / 5.99 | 5.09 | 35/360 | 34+57 | cut: Baked oil band (0.10) barely shows and costs whole-bar contrast (5.1). |
| M-r6-06 | M-r6-01 | r6-01, quieter rings (for the kitchen iPad far away) | 7 | 8 | 9 | 8 | 9 | 41 | 6.75 / 6.06 / 6.06 / 6.06 | 5.64 | 30/360 | 29+48 | top: r6-01 with quieter rings: calmest behind the words, lightest files (77 KB); for the kitchen iPad far away. |
| M-r6-07 | M-r6-01 | day set: day 2 of the r6-01 recipe (new seed) | 8 | 8 | 8 | 8 | 8 | 40 | 5.81 / 6.00 / 5.73 / 6.14 | 5.16 | 35/360 | 34+57 | day: Day 2 of the r6-01 recipe. |
| M-r6-08 | M-r6-01 | day set: day 3 of the r6-01 recipe (new seed) | 8 | 8 | 7 | 8 | 8 | 39 | 6.26 / 5.44 / 5.44 / 5.44 | 5.44 | 37/360 | 34+57 | day: Day 3; a lighter block under the mark (5.4). |
| M-r6-09 | M-r6-01 | day set: day 4 of the r6-01 recipe (new seed) | 8 | 8 | 8 | 8 | 8 | 40 | 5.99 / 6.68 / 6.03 / 6.26 | 5.40 | 43/360 | 35+59 | day: Day 4. |

<!-- /TABLES -->

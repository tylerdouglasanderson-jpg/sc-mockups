# I-007 lane N: the header bar, rounds 7-8 (final polish)

2026-11-27. 18 boards in 2 rounds (round 7: 12, round 8: 6 finals), all in ONE shared bar, plus the layout fixes from
the round-6 outside panel (V, F, L). Starting point: lane M's M-r6-01 board and shared bar.

Files: `gallery.html` (phone; before/after first, top 3, weight, day set, rounds, then the page / narrow / mark /
native sheets), `desktop.html` (before/after at 1280, then top 3 at 1280, 820, 1180, 1920, 2560), `tiles/` (every
board as `<id>@1x.webp`, `@2x`, `@3x`), `favicon-tile-n114.svg` (the pick mark), `before/endgrain-bp.svg` (today's
board, for the before shots), `results.json`, `pages_check.json`, `BUILD_NOTES.md` (the code a build lane needs).
Recipes: `gen/board_n.py` (generator), `gen/variants.py` + `variants_r8.py`, `gen/mock.py` (the one bar),
`gen/shoot.py r7|r8`, `gen/build_pages.py shots`, `gen/grades.py`, `gen/tables.py`.
Shots: scratch `.../scratchpad/i007/shots_N/` (sheets at 390 2x, 1280 true 1x, the 3x tile at 1:1).

## How it was judged

- Grades 1-10, strict (self-grades run about 1 high): **B**eauty, **E**thos (clearly warm end grain), **R**eadability,
  **F**it (rows whole, header brown family, frameLead, nothing off-palette), **T**iling + weight.
- Contrast: each width shot again with the words, mark and avatar hidden; cream `#FAF4EB` against the **single
  lightest pixel** in the box of the name, the mark and the account. Widths: 390 (3x file), 820, 1180, 1280 (2x file),
  1280 and 1920 at 1x (the new 1x file). "Whole bar worst" = lightest pixel anywhere in the 56 row at any width.
- New this lane: every tile FILE is decoded after WebP and checked pixel by pixel (see "Contrast" below).
- Looked at: 390 sheets at 2x, 1280 sheets at true 1x, the 3x tile at 1:1, every page sheet, the narrow sheet zoomed
  at 3x, the desktop page at 1x.

## Panel round 6 → what changed

| # | Finding | Fix in lane N | Where to see it |
|---|---|---|---|
| 1 | Rings machine-drawn, bullseyes stamped | Every ring its own width (lognormal + slow good/lean-year trend), its own latewood weight and share; two scales of wobble + soft lobes; soft light/dark bands every 4-8 rings; fine pores; faint rays. Hearts: 1 block in 7, never two touching (8 neighbours, wrapping), pith at or past the block edge, so rings are cut by the glue line; rings fade near the pith. | 3x sheets; r7-01 vs r8-01 |
| 2 | Flat and dim on wide screens | One step warmer and lighter (bar average #6E4019, was #663B16), hue 20-30, 3 honey/maple blocks per tile placed away from the name and from the account spots at 390/820/1180/1280/1440/1920, tone spread 0.85 under the name and 1.12 right of it. Two steps (r7-10) broke the 5:1 margin: cut. | 1280 1x sheets; desktop before/after |
| 3 | Grid reads like tile | Brick-laid (r7-02, r8-02): keeps calm, least tile-like at 1280+. Light glue edge (r7-03/04): invisible at 1x and 2x, cut. | r8-02 |
| 4 | Avatar cold, two rings | Checked the app: `Avatar.tsx` with `ring` ALREADY draws one 1.5 cream border and no dark outline. The two rings and the cold blue were lane M's mock only. Mock now matches the app (Copper fill, a warm member colour). Strip of 6 member colours shows the one ring keeps every edge. No app change needed, except maybe a warm DEFAULT colour (BUILD_NOTES). | mark sheet |
| 5 | Mark: second logo colour, weak letters | True app-icon tile (#FAF4EB, the icon file), 26 tall, "SC" 14% larger (10% and 0% shown beside it). No other mark colour. | mark sheet |
| 6 | Web needs a 1x file | 1x/2x/3x for every board; web picks with `image-set` in `webTileStyle`; weights below. 2160 wide tried (r8-06). | weight table; BUILD_NOTES |
| 7 | Pages | Sign-in drawn for real, no second wordmark. "Shared list" removed from the bar (page eyebrow instead). Leads follow `frameHeaderLead`: 16 phone, 10 slim rail, 8 wide rail. | page sheet; desktop |
| 8 | Narrow phones | Rule: (1) long timer → short form "1h 4m"; (2) timer → icon; (3) saving cloud → tiny cream cloud on the avatar (not a dot). Bar text capped (does not grow). | narrow sheet |
| 9 | Before/after | Today's live bar (720x108 SVG tiled from the top, 50 row, 22 semibold, no mark) beside the pick at 390 and 1280. The wrong line "web today = the proposed native" is gone: web today tiles from the top; native today uses cover. | gallery top; desktop top |
| 10 | Day set | 3 boards (seeds of M-r6-01, 07, 09; 08 dropped), but ONE main pick: N-r8-01. | gallery day set |

## Contrast: a new trap found and fixed

Lossy WebP keeps colour at half size. Next to fine dark detail (pores, ring edges, glue) it lifts single pixels by up
to ~30% in brightness, whatever the cap in the source: a tile capped at 6.4:1 decoded at 5.3:1, and the first
round-7 tiles fell to 4.4-4.9:1 at single pixels. Higher quality does not fix it (q90 still 5.65 from 6.4).
Fix (`encode_safe` in `board_n.py`): encode, decode, find every pixel under 5.15:1, darken the source a little around
just those spots, encode again (up to 24 times). Every shipped file is now 5.15:1 or better at every pixel, all three
densities. Any re-encode (a build step, a CDN) must re-run this check.

## Round 7 (12 boards)

What I saw:
- The new rings work: at 3x the blocks look like sawn wood (uneven rings, soft bands), not a printed record. At 1x the
  bar reads warmer and more alive than M-r6-01 (r7-01 vs control r7-12).
- A few hearts still showed three quarters of a target (pith inside the block), and a few single rings were too heavy
  ("worms"). Calmer growth (r7-08) fixed the worms.
- Pores and rays only pay at 3x; doubling them (r7-07) is invisible at 1x and costs 7 KB. Kept at the low setting.
- Light glue edge (r7-03/04): not seen. Even tone spread (r7-06): flatter right of the name. 32 px (r7-09): busier.
- Brick-laid (r7-02): calm, and the wide bar stops reading as floor tile. Kept.
Best: **N-r7-08** (41) and **N-r7-02** (41).

Changes for round 8: r7-08's calmer growth; pith at or past the block edge (0.8-1.3 of the half block); brick tried
once more; quieter version for the kitchen; day set from the same recipe; a 2160-wide tile weighed.

## Round 8 (6 finals)

What I saw:
- No stamped targets left anywhere in r8-01 at 390, 1280 or 3x; heart blocks now show rings cut by the glue line.
- r8-02 brick: on a phone it can read a little like a brick wall; on 1280+ it is the most natural.
- r8-03 quieter: the calmest and lightest (90 KB); a bit less crafted up close.
- Day boards r8-04/05: same family; r8-05 has a few soft clumps (50 near-equal pairs).
- r8-06 (2160 wide): looks the same, 175 KB instead of 113; I cannot spot the 1440 repeat on a 1920 screen at 1x.
  **Not worth it now**; make it only if Tyler sees a repeat on his 1920 screen.

Score trend (best per round, self, /50): M r4 38 → r5 40 → r6 41 (panel 7-8/10) → N r7 41 → r8 41 (expect the panel
to read the ring and warmth fixes as +1 on Beauty/Ethos; the self-grade stays 41 because I grade strict).

## Top 3

1. **N-r8-01** (41: B8 E9 R8 F8 T8) MAIN PICK, one board for "same background". Worst under words **5.30:1**,
   anywhere on the bar 5.20. 15 + 37 + 61 = **113 KB** (1x+2x+3x).
2. **N-r8-02** (41: B8 E9 R8 F8 T8) brick-laid. Worst **5.30:1** (bar 5.22). 114 KB.
3. **N-r8-03** (41: B7 E8 R9 F8 T9) quieter rings. Worst **5.35:1** (bar 5.18). 90 KB.

## Weight (budget 350 KB for one board, all densities)

- Pick 1: 1x 15 KB, 2x 37 KB, 3x 61 KB = **113 KB**. Today's SVG: 300 KB.
- A browser downloads ONE file (image-set): 15 KB (plain screen), 37 KB (2x), 61 KB (3x phone).
- The iPhone/iPad app bundles all three: 113 KB.
- Day set of 3 (r8-01, 04, 05): 341 KB, just under 350.
- 2160 wide (r8-06): 24 + 57 + 95 = 175 KB. Not worth it (above).

## Every page, the narrow phones, the mark (on pick 1)

- Contrast on every page (single lightest pixel): name 5.76, mark 5.90, account 5.81, "Sign in" 5.55, timer 5.55.
- Sign-in: bar only, nothing top right, page heading "Sign in", NO second big wordmark (DESIGN 2.5.6 changes).
- Sign-up: "Sign in" top right is a real 44-tall button. Shopper: nothing top right; "Shared list" is the page eyebrow.
- Cook: A (no board, today) and B (the bar on top) both shown; Tyler's call.
- Narrow phones (room between name and right side, need 12):
  320: timer to icon + cloud onto the avatar, 43 · 360: timer to icon, 39 ·
  375: 4:12 fits (25); 1:04:12 → "1h 4m" (13) · 390: fits (40; 1:04:12 17) · 393 (status 59): fits (43; 1:04:12 20).
- Mark: true icon tile 26, "SC" +14%. Avatar: as the app already draws it (one cream ring); Copper fill in the mock.
- Leads (frameHeaderLead): phone 16, slim rail 10 (lines up with the 44 squares), wide rail 8 (lines up with the
  rail's pills). Right side: row padding 8, so the avatar circle's edge sits ~16 from the screen edge, like the mark.

## Still weak

- Self-grades only for rounds 7-8; no outside panel yet. Expect about 1 lower per lens.
- At 320 the lit timer still folds to an icon (no time shown); the time lives in the menu and the screen reader.
- Native tiling (RN `Image` `resizeMode="repeat"` with WebP @2x/@3x) is still only mocked in a browser. It must be
  built and seen on an iPhone and an iPad before the board is called standard.
- The "SC" letters in the bar mark are 14% bigger than on the home-screen icon file (same tile, same colour, same glyph).
  If Tyler wants pixel-identical, use `icon26` (shown).
- Avatar fill is the person's own colour: a cold colour (Ocean, Cobalt) will still be cold. Only the default
  (derived) colour can be made warm; see BUILD_NOTES.
- Kitchen iPad far away and real screens: not seen on a device.
- No dark mode: the header has no dark palette entry.

## Score tables

<!-- TABLES -->
### Round 7 table

| id | from | what it tries | B | E | R | F | T | sum | worst under words 390 / 820 / 1180 / 1280 / 1280@1x / 1920@1x | whole bar worst | near-equal neighbours | hearts / honey | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| N-r7-01 | M-r6-01 | M-r6-01 with grown rings (uneven widths and weights, wobble, bands, pores, rays), hearts 1 in 7 cut by the edge, one step warmer, 3 honey blocks | 8 | 9 | 8 | 8 | 8 | 41 | 5.61 / 5.46 / 5.82 / 5.30 / 5.40 / 5.40 | 5.20 | 23/360 | 29/200 · 3 | 15+37+60 = 113 | keep: Rings finally look grown, not drawn; warmer and lighter than M-r6-01. A few hearts still show 3/4 of a target, and a few single rings are heavy. |
| N-r7-02 | N-r7-01 | r7-01 brick-laid: odd rows shifted half a block | 8 | 9 | 8 | 8 | 8 | 41 | 5.37 / 5.30 / 5.30 / 5.30 / 5.46 / 5.46 | 5.18 | 31/360 | 28/200 · 3 | 15+36+59 = 110 | keep: Brick-laid rows: the grid stops reading as floor tile at 1280. Calm. Kept for round 8. |
| N-r7-03 | N-r7-01 | r7-01 + a faint light edge inside each glue line (left and top) | 8 | 8 | 8 | 8 | 8 | 40 | 5.21 / 5.26 / 5.52 / 5.30 / 5.38 / 5.58 | 5.06 | 23/360 | 29/200 · 3 | 16+37+61 = 114 | cut: The light edge on the glue lines cannot be seen at 1x or 2x; no gain. |
| N-r7-04 | N-r7-02 x N-r7-03 | brick-laid + light glue edge | 8 | 8 | 8 | 8 | 8 | 40 | 5.23 / 5.26 / 5.49 / 5.36 / 5.52 / 5.52 | 5.13 | 33/360 | 28/200 · 3 | 15+36+59 = 110 | cut: Brick + light edge: the light edge adds nothing; keep brick alone. |
| N-r7-05 | M-r6-06 | r7-01 with quieter rings (kitchen iPad far away) | 7 | 8 | 9 | 8 | 9 | 41 | 5.82 / 5.42 / 5.81 / 5.81 / 5.55 / 5.55 | 5.20 | 21/360 | 29/200 · 3 | 12+29+49 = 90 | keep: Quieter rings: calmest behind the words, lightest files (90 KB all three). |
| N-r7-06 | N-r7-01 | r7-01, even tone spread (no split at the name), 2 honey blocks | 7 | 8 | 8 | 8 | 8 | 39 | 5.28 / 5.30 / 5.45 / 5.45 / 5.59 / 5.57 | 5.09 | 43/360 | 29/200 · 2 | 15+36+60 = 111 | cut: Even tone spread: 43 near-equal pairs, flatter right of the name. The split spread (r7-01) is better. |
| N-r7-07 | N-r7-01 | r7-01 with stronger pores and rays (do they show at 1x?) | 8 | 8 | 8 | 8 | 7 | 39 | 5.68 / 5.24 / 5.82 / 5.51 / 5.56 / 5.56 | 5.20 | 22/360 | 29/200 · 3 | 15+38+67 = 120 | cut: Stronger pores and rays still do not show at 1x; 120 KB. Fine detail only pays at 3x. |
| N-r7-08 | N-r7-01 | r7-01, calmer growth: less wobble, steadier ring widths | 8 | 9 | 8 | 8 | 8 | 41 | 5.60 / 5.36 / 5.36 / 5.36 / 5.49 / 5.49 | 5.09 | 26/360 | 29/200 · 3 | 15+38+61 = 114 | keep: Calmer growth (less wobble, steadier rings): no heavy "worm" rings, still clearly grown. Best of round 7. |
| N-r7-09 | M-r6-03 | M-r6-03 shape (32 px, firmer glue) with the new rings and warmth | 7 | 8 | 8 | 8 | 8 | 39 | 5.79 / 5.28 / 5.93 / 5.93 / 5.84 / 5.55 | 5.18 | 45/405 | 32/225 · 3 | 16+38+62 = 116 | cut: 32 px blocks are busier at 1x (45 near-equal pairs); 36 px stays. |
| N-r7-10 | N-r7-01 | r7-01, two steps lighter (tests the 5:1 cap) | 8 | 9 | 7 | 8 | 8 | 40 | 5.43 / 5.40 / 5.60 / 5.40 / 5.28 / 5.28 | 4.87 | 27/360 | 29/200 · 3 | 15+38+61 = 114 | cut: Two steps lighter: whole bar falls to 4.87:1 at one width. One step is the limit. |
| N-r7-11 | N-r7-01 | r7-01 with hearts 1 in 10 | 8 | 8 | 8 | 8 | 8 | 40 | 5.55 / 5.39 / 5.39 / 5.39 / 5.43 / 5.43 | 5.16 | 21/360 | 20/200 · 3 | 15+36+60 = 112 | keep: Hearts 1 in 10: calm, a little less "end grain" at a glance. 1 in 7 cut by the edge (r8) is better. |
| N-r7-12 | N-r7-01 | r7-01 in lane M amber (not warmer): isolates the colour step | 7 | 8 | 9 | 8 | 8 | 40 | 6.13 / 5.91 / 6.39 / 5.90 / 6.09 / 6.09 | 5.20 | 39/360 | 29/200 · 3 | 15+36+57 = 108 | control: Lane M amber with the new rings: darker and browner than r7-01 at 1280. Shows the warm step is real. |

### Round 8 table

| id | from | what it tries | B | E | R | F | T | sum | worst under words 390 / 820 / 1180 / 1280 / 1280@1x / 1920@1x | whole bar worst | near-equal neighbours | hearts / honey | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| N-r8-01 | N-r7-08 | MAIN PICK: calmer grown rings, hearts 1 in 7 cut by the block edge, one step warmer, 3 honey blocks | 8 | 9 | 8 | 8 | 8 | 41 | 5.49 / 5.30 / 5.76 / 5.62 / 5.35 / 5.64 | 5.20 | 30/360 | 29/200 · 3 | 15+37+61 = 113 | top: MAIN PICK. Grown rings, hearts cut by the block edge (no stamped targets), one step warmer, honey blocks away from the words. 5.3:1 worst under words, 5.2 anywhere. |
| N-r8-02 | N-r8-01 x N-r7-02 | r8-01 brick-laid (odd rows shifted half a block) | 8 | 9 | 8 | 8 | 8 | 41 | 5.55 / 5.51 / 5.49 / 5.77 / 5.59 / 5.30 | 5.22 | 37/360 | 28/200 · 3 | 16+38+61 = 114 | top: r8-01 brick-laid: least like tile at 1280 and 1920; on a phone it can read a little like a brick wall. |
| N-r8-03 | N-r8-01 x N-r7-05 | r8-01 with quieter rings (kitchen iPad far away) | 7 | 8 | 9 | 8 | 9 | 41 | 5.55 / 5.35 / 5.81 / 5.63 / 5.59 / 5.66 | 5.18 | 27/360 | 29/200 · 3 | 12+30+49 = 90 | top: r8-01 with quieter rings: calmest, lightest files (90 KB); for the kitchen iPad far away. |
| N-r8-04 | N-r8-01 (M-r6-07 seed) | day set: day 2 of the r8-01 recipe | 8 | 8 | 8 | 8 | 8 | 40 | 5.52 / 5.39 / 5.55 / 5.88 / 5.88 / 5.31 | 5.18 | 42/360 | 29/200 · 3 | 15+38+62 = 115 | day: Day 2 of the r8-01 recipe. Same family, a little cooler. |
| N-r8-05 | N-r8-01 (M-r6-09 seed) | day set: day 3 of the r8-01 recipe | 8 | 8 | 8 | 8 | 8 | 40 | 5.70 / 5.56 / 5.47 / 5.72 / 5.83 / 5.70 | 5.12 | 50/360 | 29/200 · 3 | 15+37+60 = 113 | day: Day 3 of the r8-01 recipe. 50 near-equal pairs: a few soft clumps. |
| N-r8-06 | N-r8-01 | r8-01 as a 2160-wide tile (no repeat on 1920 screens): is it worth the weight? | 8 | 9 | 8 | 8 | 7 | 40 | 5.34 / 5.36 / 5.36 / 5.36 / 5.23 / 5.23 | 5.21 | 49/540 | 43/300 · 4 | 24+57+94 = 175 | cut: 2160-wide tile: no repeat on 1920 screens, but 175 KB vs 113 and I cannot see the 1440 repeat at 1x. Not worth it now. |

<!-- /TABLES -->

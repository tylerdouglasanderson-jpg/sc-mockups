# I-007 lane B: bolder cutting boards (rounds 1-3)

Builder: lane B (board texture only, bolder departures). 2026-11-27.
Grades are 1-10: B = beauty, E = ethos (clearly end grain, warm wood), R = readability, F = fit, T = tiling and file weight.
I tried to grade strictly; self-grades still tend to run about a point high.
"Mock contrast" = the worst cream-to-wood ratio behind the wordmark at 1280, 820, 390 (phone) and 1180 (iPad); 4.5 is the bar.
"Tile worst" = the single lightest pixel anywhere in the tile, which is stricter than what sits behind the words.

## How it is made
- `gen/boardgen.py`: a raster generator. Draws at 4 px per CSS px and shrinks to a 2x WebP (1440x216, used at 720x108 CSS like today).
  Every noise layer is FFT-based, so it wraps around by itself. Lighting uses `np.roll`, and knife marks are drawn three times
  with wrap-around, so the tile has no seam. Blocks that cross the right edge wrap to the left.
- Layouts: grid, brick, stagger, and "strips" (a real board: strips of different widths glued together, cut into rows,
  each row slid and/or flipped).
- Contrast guard: a soft squeeze on brightness plus a hard cap after shrinking, so cream text always has 4.5:1 or better.
- `gen/boardgen_v1.py` made round 1 (copied before the v2 changes). Rounds 2-3 use `gen/boardgen.py`. Variants live in `gen/variants.py`.
- `gen/shoot.py` takes the mock shots and measures contrast; `gen/sheets.py` makes the seam strips and zoom sheets;
  `gen/export3x.py` makes 3x files; `gen/build_pages.py` writes gallery.html and desktop.html.
- Baseline: today's `endgrain-bp.svg` (LIVE) graded B6 E8 R8 F8 T5. It is clearly end grain, but it is a flat vector with
  perfect target rings and weighs 300 KB. Mock contrast 5.37.

## Round 1 (14 boards, generator v1)
| id | tries | B E R F T | avg | mock contrast | KB | verdict |
|---|---|---|---|---|---|---|
| B-r1-01 | real strip board, walnut/cherry/maple, rows slid + flipped | 6 6 7 7 8 | 6.8 | 4.71 | 19 | keep |
| B-r1-02 | walnut + maple squares, checkerboard ring turns | 5 5 7 7 8 | 6.4 | 4.55 | 21 | cut: maple turns khaki pixels |
| B-r1-03 | big 36 px blocks, ring centre in each | 5 6 8 6 8 | 6.6 | 5.45 | 14 | keep (idea), muddy colours |
| B-r1-04 | brick rows | 5 5 7 7 8 | 6.4 | 4.96 | 15 | cut: reads as a brick wall |
| B-r1-05 | hand-planed, slipping rows, tilted blocks | 5 5 7 7 8 | 6.4 | 4.66 | 20 | cut: busy, patchy |
| B-r1-06 | knife-scored | 5 5 7 7 8 | 6.4 | 4.66 | 16 | cut: marks invisible; same as 01 |
| B-r1-07 | oiled sheen, lit from top left | 6 6 7 8 8 | 7.0 | 4.77 | 23 | keep |
| B-r1-08 | cherry + mahogany, 30x27 | 4 4 8 6 8 | 6.0 | 5.25 | 11 | cut: terracotta tiles |
| B-r1-09 | tiny 12 px five-wood mosaic | 3 4 6 6 8 | 5.4 | 4.66 | 20 | cut: noise |
| B-r1-10 | two tall rows of wide strips | 4 3 7 6 8 | 5.6 | 4.71 | 11 | cut: reads as planks |
| B-r1-11 | today's colours, ring arcs not targets | 6 6 7 8 8 | 7.0 | 4.73 | 15 | keep |
| B-r1-12 | oak + walnut, ray flecks | 5 5 7 7 8 | 6.4 | 4.79 | 21 | cut: flecks invisible, khaki |
| B-r1-13 | dark walnut, thin maple pin stripes | 6 6 8 7 8 | 7.0 | 4.61 | 21 | keep |
| B-r1-14 | flipped strip board, 27 px rows | 5 5 8 7 8 | 6.6 | 5.24 | 17 | keep |

What I learned by looking:
- The rings were far too faint. Today's board wins on "this is end grain" because you can see its rings.
- Ring centres set far outside the block draw almost straight lines, which read as planks, not end grain.
- Light woods (maple) went olive/khaki when the contrast guard darkened them, because darkened yellow looks green.
- Cherry at full colour looked like terracotta tile. Knife marks and sheen were invisible at real size.
- Tiles are tiny (11-23 KB) and every one wraps with no seam.

Changes for round 2 (generator v2): new woods tuned to sit under the cap from the start (honey maple, not yellow);
latewood bands wider and darker; rings spaced wider so they show at 1x; ring centres just off the block (curved arcs);
knife marks get a dark hairline.

## Round 2 (12 boards, generator v2)
| id | tries | B E R F T | avg | mock contrast | KB | verdict |
|---|---|---|---|---|---|---|
| B-r2-04 | big 36 px blocks, today's colours, ring centres | 8 8 8 8 8 | 8.0 | 4.83 | 22 | **lead** |
| B-r2-05 | today's 18 px grid, real curved rings | 7 8 7 8 8 | 7.6 | 4.84 | 26 | keep |
| B-r2-11 | checkerboard ring turns, today's colours | 7 7 7 8 8 | 7.4 | 4.80 | 26 | keep (as plain grid) |
| B-r2-03 | 24x27 blocks, centres + arcs, mixed woods | 6 7 7 7 8 | 7.0 | 4.64 | 23 | keep |
| B-r2-08 | strip board, 27 px rows, slid + flipped | 6 7 7 7 8 | 7.0 | 4.62 | 23 | keep |
| B-r2-10 | chunky board, wide strips | 6 7 7 7 8 | 7.0 | 4.96 | 23 | keep |
| B-r2-01 | strip board with visible rings | 6 7 7 7 8 | 7.0 | 4.89 | 25 | cut: flat honey blocks pop |
| B-r2-02 | calmer strip board | 6 7 7 7 8 | 7.0 | 4.64 | 24 | cut: same problem |
| B-r2-07 | dark walnut strip board | 6 6 8 7 8 | 7.0 | 5.62 | 26 | cut: wavy rings look like a fingerprint |
| B-r2-09 | strip board + knife marks | 6 7 7 7 8 | 7.0 | 4.72 | 27 | cut: marks still only show up close |
| B-r2-12 | r2-01 recipe, new seed | 6 7 7 7 8 | 7.0 | 4.71 | 25 | cut (the recipe does hold for a second day) |
| B-r2-06 | raised late rings + oiled shine | 5 7 6 7 6 | 6.2 | 4.52 | 48 | cut: embossed halos, tile worst 3.97 |

What I learned: big blocks with visible ring centres in today's colour family (r2-04) look the most like a real, warm board
and stay calm behind the words. Mixing in a different wood makes blocks jump. Relief lighting looks fake at this size.
The rings were still a bit wavy ("contour map").

Changes for round 3: less ring wobble and warping, softer and wider bands, slightly lower ring contrast; a lower cap
(0.146) so the whole tile, not just the wordmark area, passes 4.5:1; a five-day set from one recipe.

## Round 3 (14 boards)
| id | tries | B E R F T | avg | mock contrast | tile worst | KB | verdict |
|---|---|---|---|---|---|---|---|
| B-r3-12 | day set: warm walnut lean | 8 8 9 8 8 | 8.2 | 6.24 | 5.38 | 20 | **top 2** |
| B-r3-01 | r2-04 refined, calmer rings | 8 8 8 8 8 | 8.0 | 5.01 | 4.62 | 21 | **top 1** |
| B-r3-06 | r3-01 + fine knife marks | 8 8 8 8 8 | 8.0 | 5.01 | 4.63 | 21 | keep (marks only show on phones) |
| B-r3-07 | day set: day 2, new blocks | 8 8 8 8 8 | 8.0 | 4.97 | 4.47 | 20 | keep (day set) |
| B-r3-14 | day set: honey lean, rings kept | 8 8 8 8 8 | 8.0 | 4.90 | 4.63 | 20 | keep (day set) |
| B-r3-03 | 36x27 blocks: two rows on web | 7 8 8 8 8 | 7.8 | 5.07 | 4.35 | 21 | **top 3** |
| B-r3-11 | big blocks in brick rows | 7 8 8 8 8 | 7.8 | 4.83 | 4.57 | 21 | keep |
| B-r3-13 | day set: warm cherry lean | 7 8 8 8 8 | 7.8 | 4.88 | 4.67 | 21 | keep (a few rusty blocks) |
| B-r3-04 | r2-05 refined, 18 px grid | 7 8 7 8 8 | 7.6 | 4.91 | 4.56 | 24 | keep: closest to today |
| B-r3-05 | 24x27, centres + arcs | 7 7 8 8 8 | 7.6 | 4.87 | 4.58 | 22 | keep |
| B-r3-09 | day set: cherry lean (v2 cherry) | 7 7 8 8 8 | 7.6 | 4.88 | 4.60 | 20 | cut: pink blocks, fixed in r3-13 |
| B-r3-02 | r3-01 + walnut and cherry mixed in | 6 7 8 7 8 | 7.2 | 4.94 | 4.69 | 21 | cut: grey-mauve blocks |
| B-r3-08 | day set: walnut lean (v2 walnut) | 6 7 8 7 8 | 7.2 | 5.93 | 5.38 | 21 | cut: grey, fixed in r3-12 |
| B-r3-10 | day set: honey lean (v2 maple) | 6 7 8 8 8 | 7.4 | 4.84 | 4.57 | 17 | cut: flat honey, fixed in r3-14 |

3x files for native (iPad cover-fit stretches 2x): `tiles/3x/` for r3-01, 03, 07, 12, 13, 14, about 39 KB each
(today's SVG is 300 KB).

## Top 3
1. **B-r3-01** (8.0): today's warm colours, big 36 px blocks, soft real rings with the centre showing. Mock contrast 5.01. 21 KB.
2. **B-r3-12** (8.2 but moodier): the walnut day. Darkest and easiest to read (6.24).
3. **B-r3-03** (7.8): the same recipe with 36x27 blocks, so the 50 px web bar shows about two rows, not one row plus a strip.
Day set: r3-01, r3-07, r3-12, r3-13, r3-14 (house, house, walnut, cherry, honey).

## Still weak / for the merge
- The web bar shows only the top 50 px of the 108 px tile (CSS size 720x108). With 36 px blocks you see one row plus a
  14 px strip at the bottom edge. If the tile were 720x100 with 25 px blocks, the web bar would show exactly two rows.
  That needs a one-line change to `webTileStyle` (not this lane's file).
- The native iPad cover-fit blows the tile up 1.64x; ship the 3x file there, or a wider native tile.
- Knife marks and oil sheen only show on phone-sized pixels; at 1x on a computer they disappear.
- Mixed species (true walnut, cherry, maple) look wrong next to the house orange-brown: grey, pink or khaki. The warm "w"
  versions fix that, but they are really tints of one wood, not a true species mix.
- The tile repeats every 720 px. I could not spot it at 1280, but a wider tile would be safer for big screens.
- No dark mode check: the app's header has no dark palette entry to test against.

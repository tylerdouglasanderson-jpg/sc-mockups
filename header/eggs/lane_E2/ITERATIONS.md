# I-007 part E, lane E2: header-board Easter eggs (rounds 1-3)

2026-11-27. Tyler (17:27): "one board, but ... things chopped up on it from time to time ... a number of variations ...
like little Easter eggs ... chopped chives, some chopped onions ... chopped herbs that are scattered about ... very
light in the background so it doesn't obscure things ... general and diffuse."

34 eggs in 3 rounds (16, 10, 8 finals). Direction of this lane: painterly / photo-like (soft raster bits with real light,
tiny wet highlights, contact shadows, some bits out of focus, juice specks), plus themed eggs.

## Files

- `gallery.html` (phone; self-contained, about 2.9 MB): base first, top 3 as LIVE bars (real tiles embedded, drawn
  at the phone's own density) + 3x close-ups, the "how often" proposal, then rounds 3, 2, 1 (390 shots + close-ups).
- `desktop.html` (self-contained, about 1 MB): base and top 3 live at 1280, 820 and 1180.
- `tiles/E2-r<n>-<nn>@1x/@2x/@3x.webp`: every egg (1440x140 CSS tile), plus `N-r8-01` (the base, copied).
- `results.json`: per egg: tile weights, file checks, contrast per width, grades.
- `gen/`: `egg.py` (the generator), `eggs.py` + `eggs_r2.py` + `eggs_r3.py` (recipes), `shoot.py` (bar shots +
  contrast), `grades.py`, `build_pages.py`, `check_pages.py`, `sheet.py` / `zoom.py` (look sheets),
  `board_n.py` (copy of lane N's generator: the base is rendered from its own recipe, seed 504) and `mock.py`
  (lane N's committed round-8 bar: 56 row, SC mark, 24 bold italic name, account top right, 1 px rule; plus
  status-bar text measuring). Shots: scratch `.../scratchpad/i007/shots_E2/`.
- Rounds 1 and 2 tiles were made by earlier states of `egg.py` (round 2 fixes, round 3 size/phone knobs); re-running
  `egg.py r1` now would draw them a little differently. Round 3 is exactly reproducible.

## How an egg is made

1. Render N-r8-01 from lane N's recipe at 3x (not the shipped WebP, so no double compression).
2. Draw each bit at 3x in linear light from a distance field (chive = rounded rod with pale cut ends; onion = a curved
   slice of one layer, glassy; herbs = jagged flakes with straight knife cuts and a vein; pepper = cracked grain with
   a paler broken face; and so on). A dome height gives a surface normal; light from the top left gives shading and
   a wet highlight; an edge light brightens the side facing the light and darkens the far side; a soft contact
   shadow falls down-right; some bits are blurred (out of focus). Colours muted 20% toward a warm grey.
3. Scatter: none over the name and mark (tile x < 195, fading in to 255); one drift where a 390 phone shows it
   (x 215-305, between the name and the avatar), the rest spread evenly along the bar; mostly in the bottom 56
   (what every bar shows), some in the phone status band; fewer in the account corners. Bits wrap at the tile
   edge (no seam).
4. Contrast: every bit is soft-capped so cream #FAF4EB stays 5.15:1 or better at every pixel (the cap never darkens
   the wood). Only tiny glints may go lighter (to 3:1), and never in the name zone (x < 345) or the account corners
   at 21 common widths (320-2560). After WebP encoding each file is decoded and checked pixel by pixel against that
   map; spots that fail are darkened and re-encoded (lane N's trick, masked).
5. Shoot in the real bar at 390 (3x, 47 status bar), 820 and 1180 (iPad, 2x), 1280 (2x), 1280 and 1920 (1x), with
   the words hidden: the single lightest pixel behind the name, mark, account and the phone's clock and battery.

## Round 1 (16): what I saw

- Phones showed NOTHING: the name zone (to 345) plus the 390 avatar corner covered the whole 0-390 slice of the
  tile. Biggest miss of the round.
- Chives read. Onion came out as grey paper scraps. Parsley as little green stars. Pepper vanished (dark on dark,
  red on red). Flour = grey blotchy smears. Scallion rings = drawn bubbles. Bell pepper and mirepoix = confetti.
  Soft focus (r1-15) made the chives feel photographed.

## Round 2 (10): changes and what I saw

Changes: a phone drift; colours muted; knife-cut flakes; glassy onion (thin body, lit edge); bigger cracked pepper
with broken faces and brighter chili; fine-powder flour; scallions rebuilt; a bug fixed (the cap darkened light wood
blocks under flour into hard-edged patches; now the cap never goes below the wood).
Saw: phones show 2-5 bits; chives and onion believable at 3x; pepper reads; flour no longer blotchy but only a faint
haze; scallions read as crumbs (cut, second miss); rosemary + salt too faint (cut).

## Round 3 (8 finals): changes and what I saw

Changes: bits 8-15% larger; +15% of each mix in the phone drift; sage less frosted and fewer ribbons.
Saw: a clear small drift between the name and the avatar on a phone; on 1280 at 1x the eggs are fine flecks across
the bar and the board still reads first. Flour is still the weak one.

Score trend (best per round, self, /50): r1 36 -> r2 38 -> r3 41.

## Top 3

1. **E2-r3-01 chives** (41: B8 F8 L8 R9 T8). Worst behind any word **5.51:1**. 15.8 + 38.4 + 62.9 = **117 KB**.
2. **E2-r3-02 onion and chive** (40: B8 F7 L8 R9 T8). Worst **5.35:1**. **116.5 KB**.
3. **E2-r3-05 pepper** (40: B7 F8 L8 R9 T8). Worst **5.30:1**. **116.7 KB**.

Every final: worst behind words 5.24-5.51:1 (every width, after encoding), 114-117 KB for all three files (budget 150).
"Whole bar worst" (3.5-5.2) is only tiny glints in the open wood, never behind a word at the checked widths.

## How often (proposal)

- About 1 day in 7 shows an egg; the other days show the plain N-r8-01.
- Picked by the date, the same way as `boardVariantIndex` in `src/components/Header.tsx`: h = FNV-1a over the local
  "YYYY-MM-DD"; egg day when `h % 7 === 0`; which egg = `Math.floor(h / 7) % EGGS.length`. Same board on every
  screen and device that day, changes at the person's own midnight, never animated.
- Sketch: `const h = fnv(dateKey); return h % 7 === 0 ? EGGS[Math.floor(h / 7) % EGGS.length] : BASE;`
- Weight: the iPhone/iPad app bundles 8 eggs x ~116 KB = ~0.93 MB on top of the base (or ship 3-5 eggs). Web loads
  one file only on an egg day (15 / 38 / 63 KB by screen density).
- With a pure hash some eggs can go months unseen (next 12 weeks: 12 egg days, chives never). If Tyler wants each egg
  seen in turn, pick by the egg-day count instead (needs a fixed start date). Calendar at the end.

## Still weak

- Flour (r3-06): a faint haze at 1x, barely visible on a phone. Needs a different idea (a sifted drift along the
  bottom edge, a dusted hand-print edge) or cut it.
- Autumn sage still a little grey; the pumpkin seeds carry it.
- At 1x (1280/1920 plain screens) every egg is small flecks: "diffuse", but you have to look. Right for an Easter
  egg, maybe too quiet for some.
- Self-grades only; no outside panel. Expect about 1 lower per lens.
- Lane E2 uses lane N's committed round-8 bar (24 bold italic Plex, mark letters +14%). Lane N's working copy has since
  moved to Fraunces 22 + the true icon file (round 9, not committed). The eggs keep the name zone clear either way;
  re-shoot with the round-9 mock once it lands.
- Native tiling of the egg tiles is only mocked in a browser (same as the base).

## Score tables

### Round 1

| id | from | what it tries | B | F | L | R | T | sum | worst behind words 390 / 820 / 1180 / 1280 / 1280@1x / 1920@1x | whole bar worst | bits | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E2-r1-01 | N-r8-01 | chives: cut rods and a few end-on rings, juice specks | 6 | 6 | 8 | 9 | 6 | 35 | 5.7 / 5.35 / 5.7 / 5.55 / 5.3 / 5.59 | 3.51 | 70 | 15.5+38.0+62.6 = 116.1 | cut: chives read, but too few and nothing on a phone |
| E2-r1-02 | N-r8-01 | onion and chive: white onion dice (translucent, wet edge) with chives | 6 | 5 | 8 | 9 | 6 | 34 | 5.81 / 5.35 / 5.45 / 5.35 / 5.42 / 5.42 | 3.92 | 74 | 15.6+37.8+61.2 = 114.6 | keep: chives fine; onion reads as grey paper scraps |
| E2-r1-03 | N-r8-01 | herb garden: parsley flakes, thyme leaves, rosemary bits, dill fronds | 6 | 5 | 8 | 9 | 6 | 34 | 5.59 / 5.46 / 5.81 / 5.4 / 5.35 / 5.76 | 4.36 | 97 | 15.5+37.6+62.3 = 115.4 | keep: parsley flakes look like little green stars (clip-art) |
| E2-r1-04 | N-r8-01 | autumn: sage (chiffonade and chopped leaf) with pumpkin seeds | 6 | 6 | 8 | 9 | 6 | 35 | 5.66 / 5.22 / 5.7 / 5.35 / 5.35 / 5.35 | 4.26 | 43 | 15.8+37.7+60.8 = 114.3 | keep: pumpkin seeds believable; sage ribbons too frosty |
| E2-r1-05 | N-r8-01 | pepper: cracked black pepper, chili flakes and seeds, a few salt flakes | 5 | 5 | 9 | 9 | 6 | 34 | 5.49 / 5.32 / 5.76 / 5.6 / 5.51 / 5.77 | 4.32 | 200 | 15.5+38.1+61.8 = 115.4 | keep: almost invisible; pepper dark on dark wood, chili red on red |
| E2-r1-06 | N-r8-01 | flour dusting: soft drifts, fine grains, small clumps | 4 | 4 | 6 | 9 | 5 | 28 | 5.4 / 5.32 / 5.7 / 5.64 / 5.43 / 5.45 | 5.21 | 26 | 15.4+38.0+62.2 = 115.6 | keep (rebuild): flour came out as grey blotchy smears |
| E2-r1-07 | N-r8-01 | scallion rings: green and white rings | 5 | 4 | 8 | 9 | 5 | 31 | 5.56 / 5.33 / 5.62 / 5.21 / 5.35 / 5.48 | 3.65 | 36 | 15.4+37.8+61.1 = 114.3 | keep (rebuild): scallion rings look like drawn bubbles |
| E2-r1-08 | N-r8-01 | red onion and parsley | 6 | 5 | 8 | 9 | 6 | 34 | 5.68 / 5.59 / 5.78 / 5.68 / 5.38 / 5.48 | 4.0 | 70 | 15.7+37.1+60.7 = 113.5 | cut: red onion too faint to tell; parsley as r1-03 |
| E2-r1-09 | N-r8-01 | cilantro and lime zest | 6 | 6 | 8 | 9 | 6 | 35 | 5.57 / 5.32 / 5.55 / 5.55 / 5.59 / 5.64 | 4.17 | 72 | 15.5+37.7+61.0 = 114.2 | keep: cilantro and lime read as herbs |
| E2-r1-10 | N-r8-01 | bell pepper dice: red, yellow and green | 5 | 5 | 7 | 9 | 4 | 30 | 5.64 / 5.4 / 5.73 / 5.49 / 5.23 / 5.23 | 3.55 | 26 | 15.5+37.5+61.1 = 114.1 | cut: red pepper squares read as confetti |
| E2-r1-11 | N-r8-01 | gremolata: parsley, minced garlic, lemon zest | 6 | 6 | 8 | 9 | 6 | 35 | 5.81 / 5.32 / 5.63 / 5.35 / 5.51 / 5.55 | 4.0 | 110 | 15.6+37.9+60.8 = 114.3 | keep: gremolata, three things that belong together |
| E2-r1-12 | N-r8-01 | mirepoix: carrot, celery, onion | 5 | 5 | 7 | 9 | 4 | 30 | 5.59 / 5.42 / 5.85 / 5.77 / 5.35 / 5.48 | 3.66 | 50 | 15.4+37.6+61.2 = 114.2 | cut: orange cubes and celery arcs read as confetti |
| E2-r1-13 | N-r8-01 | rosemary and sea salt | 6 | 6 | 9 | 9 | 6 | 36 | 5.6 / 5.55 / 5.62 / 5.42 / 5.31 / 5.55 | 3.97 | 66 | 15.5+37.5+61.6 = 114.6 | keep: quiet, rosemary needles believable |
| E2-r1-14 | N-r8-01 | basil ribbons and cracked pepper | 5 | 5 | 8 | 9 | 5 | 32 | 5.74 / 5.35 / 5.7 / 5.55 / 5.31 / 5.55 | 4.55 | 104 | 15.6+37.8+60.9 = 114.3 | cut: basil ribbons read as green string |
| E2-r1-15 | N-r8-01 | chives, photo depth: a third of the bits out of focus | 6 | 6 | 9 | 9 | 6 | 36 | 5.57 / 5.3 / 5.7 / 5.68 / 5.35 / 5.43 | 4.01 | 70 | 15.6+37.8+62.0 = 115.4 | keep: soft-focus bits feel like a photo; merge with r1-01 |
| E2-r1-16 | N-r8-01 | baker's board: flour drifts with a few parsley flakes | 4 | 4 | 6 | 9 | 5 | 28 | 5.44 / 5.26 / 5.77 / 5.35 / 5.35 / 5.4 | 5.16 | 36 | 15.8+38.0+62.8 = 116.6 | cut: flour smears as r1-06 |

### Round 2

| id | from | what it tries | B | F | L | R | T | sum | worst behind words 390 / 820 / 1180 / 1280 / 1280@1x / 1920@1x | whole bar worst | bits | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E2-r2-01 | E2-r1-01 x E2-r1-15 | chives: more of them, a quarter out of focus (r1-01 x r1-15) | 7 | 7 | 8 | 9 | 7 | 38 | 5.51 / 5.4 / 5.64 / 5.28 / 5.43 / 5.64 | 4.17 | 95 | 15.7+38.0+61.0 = 114.7 | keep: chopped chives with cut ends; a few soft-focus |
| E2-r2-02 | E2-r1-02 | onion and chive: glassy onion dice with chives | 7 | 7 | 8 | 9 | 7 | 38 | 5.59 / 5.34 / 5.7 / 5.39 / 5.49 / 5.54 | 3.57 | 75 | 15.5+38.4+61.4 = 115.3 | keep: onion now glassy slivers beside the chives |
| E2-r2-03 | E2-r1-03 | herb garden: knife-cut parsley, thyme, rosemary, dill | 6 | 6 | 9 | 9 | 7 | 37 | 5.68 / 5.29 / 5.57 / 5.57 / 5.59 / 5.73 | 4.88 | 97 | 15.2+37.5+60.7 = 113.4 | keep: knife-cut parsley reads; very faint at 1x |
| E2-r2-04 | E2-r1-04 | autumn: sage bits and ribbons with pumpkin seeds | 7 | 6 | 8 | 9 | 6 | 36 | 5.68 / 5.3 / 5.7 / 5.43 / 5.35 / 5.64 | 4.27 | 43 | 15.8+37.8+60.9 = 114.5 | keep: sage still a bit frosted, too many ribbons |
| E2-r2-05 | E2-r1-05 | pepper: cracked pepper with broken faces, chili flakes and seeds, flaky salt | 6 | 7 | 9 | 9 | 7 | 38 | 5.81 / 5.24 / 5.77 / 5.63 / 5.35 / 5.51 | 3.56 | 202 | 15.6+38.3+61.8 = 115.7 | keep: cracked pepper with broken faces reads; chili still quiet |
| E2-r2-06 | E2-r1-06 | flour dusting: fine powder in soft drifts, a few pinches | 6 | 5 | 7 | 9 | 6 | 33 | 5.49 / 5.3 / 5.76 / 5.59 / 5.46 / 5.46 | 5.21 | 16 | 15.1+37.9+62.1 = 115.1 | keep: no more blotches; still a faint haze, nothing on a phone |
| E2-r2-07 | E2-r1-13 | rosemary and flaky sea salt | 6 | 5 | 9 | 9 | 6 | 35 | 5.68 / 5.42 / 5.73 / 5.49 / 5.43 / 5.81 | 3.54 | 72 | 15.4+37.8+60.8 = 114.0 | cut: too faint to say what it is |
| E2-r2-08 | E2-r1-09 | cilantro and lime zest | 6 | 6 | 9 | 9 | 7 | 37 | 5.63 / 5.3 / 5.93 / 5.35 / 5.4 / 5.43 | 4.15 | 72 | 15.4+38.1+61.6 = 115.1 | keep: cilantro and lime, quiet |
| E2-r2-09 | E2-r1-11 | gremolata: parsley, minced garlic, lemon zest | 7 | 6 | 9 | 9 | 7 | 38 | 5.57 / 5.31 / 5.53 / 5.22 / 5.51 / 5.49 | 3.68 | 108 | 15.6+38.1+60.6 = 114.3 | keep: gremolata, garlic bits add a pale note |
| E2-r2-10 | E2-r1-07 x E2-r1-01 | spring onion: scallion rings (green and white) with chives | 5 | 4 | 8 | 9 | 5 | 31 | 5.68 / 5.58 / 5.7 / 5.32 / 5.4 / 5.4 | 3.92 | 56 | 15.5+37.7+60.7 = 113.9 | cut: scallion rings read as crumbs (second miss) |

### Round 3

| id | from | what it tries | B | F | L | R | T | sum | worst behind words 390 / 820 / 1180 / 1280 / 1280@1x / 1920@1x | whole bar worst | bits | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E2-r3-01 | E2-r2-01 | chives (final): cut rods, a few rings, a quarter soft-focus, juice specks | 8 | 8 | 8 | 9 | 8 | 41 | 5.61 / 5.51 / 5.81 / 5.68 / 5.59 / 5.59 | 3.46 | 109 | 15.8+38.4+62.9 = 117.1 | top: chopped chives, the clearest "someone was cooking"; quiet at 1x |
| E2-r3-02 | E2-r2-02 | onion and chive (final): glassy onion dice with chives | 8 | 7 | 8 | 9 | 8 | 40 | 5.62 / 5.38 / 5.7 / 5.7 / 5.35 / 5.42 | 3.92 | 86 | 15.6+38.2+62.7 = 116.5 | top: onion and chive, Tyler's own example; onion slivers glassy |
| E2-r3-03 | E2-r2-03 | herb garden (final): knife-cut parsley, thyme, rosemary, dill | 7 | 7 | 9 | 9 | 8 | 40 | 5.68 / 5.48 / 5.7 / 5.6 / 5.35 / 5.48 | 4.09 | 120 | 15.4+37.6+60.9 = 113.9 | final: herb garden, the quietest of the green ones |
| E2-r3-04 | E2-r2-04 | autumn (final): sage bits and a few ribbons, pumpkin seeds | 7 | 6 | 8 | 9 | 7 | 37 | 5.36 / 5.24 / 5.85 / 5.68 / 5.43 / 5.48 | 4.07 | 51 | 15.8+37.8+62.3 = 115.9 | final: autumn; pumpkin seeds good, sage still a little grey |
| E2-r3-05 | E2-r2-05 | pepper (final): cracked pepper, chili flakes and seeds, flaky salt | 7 | 8 | 8 | 9 | 8 | 40 | 5.62 / 5.41 / 5.43 / 5.45 / 5.3 / 5.3 | 4.12 | 232 | 15.7+38.1+62.9 = 116.7 | top: cracked pepper, chili and salt; the one non-green egg that works |
| E2-r3-06 | E2-r2-06 | flour (final): fine powder drifts and a few pinches | 5 | 5 | 8 | 9 | 6 | 33 | 5.59 / 5.34 / 5.73 / 5.27 / 5.24 / 5.68 | 5.21 | 18 | 15.2+37.8+61.3 = 114.3 | final (weak): flour is a faint haze at 1x, hardly seen on a phone |
| E2-r3-07 | E2-r2-09 | gremolata (final): parsley, minced garlic, lemon zest | 7 | 7 | 9 | 9 | 8 | 40 | 5.68 / 5.3 / 5.71 / 5.59 / 5.35 / 5.48 | 3.56 | 124 | 15.5+38.1+60.9 = 114.5 | final: gremolata |
| E2-r3-08 | E2-r2-08 | cilantro and lime (final) | 7 | 7 | 9 | 9 | 8 | 40 | 5.68 / 5.36 / 5.68 / 5.38 / 5.35 / 5.48 | 4.0 | 83 | 15.8+37.8+61.3 = 114.9 | final: cilantro and lime |

### Egg days, next 12 weeks (from 2026-11-28)

- 2026-12-01 (Tue): E2-r3-02
- 2026-12-08 (Tue): E2-r3-05
- 2026-12-13 (Sun): E2-r3-05
- 2026-12-27 (Sun): E2-r3-02
- 2026-12-31 (Thu): E2-r3-05
- 2027-01-02 (Sat): E2-r3-08
- 2027-01-14 (Thu): E2-r3-03
- 2027-01-20 (Wed): E2-r3-08
- 2027-01-29 (Fri): E2-r3-03
- 2027-02-03 (Wed): E2-r3-08
- 2027-02-11 (Thu): E2-r3-03
- 2027-02-18 (Thu): E2-r3-08

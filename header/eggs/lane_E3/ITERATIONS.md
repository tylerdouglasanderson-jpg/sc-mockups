# I-007 part E, lane E3 (merge): header-board Easter eggs, rounds 4-8

2026-11-27. 49 tiles in 5 rounds: round 4 (13 eggs), round 5 (10), round 6 (6 finals x faint / medium = 12),
round 7 (the outside panel's fixes: 5 eggs medium + 1 faint twin = 6), round 8 (the final set, 5 eggs, medium).
Tyler's ask (11-27 17:27): "chopped chives, some chopped onions ... chopped herbs that are scattered about ... very
light in the background so it doesn't obscure things ... very general and diffuse."

## The final set (round 8, medium, in turn order)

| turn | egg | id | self /50 | worst cream, every px, 320-2560 | gold | food behind words (11 widths) | KB 1x+2x+3x |
|---|---|---|---|---|---|---|---|
| 1 | chives | E3-r8-01 | 40 | 5.16:1 | 3.04:1 | 0% | 16.2+38.8+62.2 = 117.2 |
| 2 | parsley | E3-r8-04 | 38 | 5.2:1 | 3.06:1 | 0% | 16.1+38.7+62.3 = 117.1 |
| 3 | chives + white onion | E3-r8-02 | 36 | 5.18:1 | 3.05:1 | 0% | 16.1+37.8+61.3 = 115.2 |
| 4 | red onion | E3-r8-03 | 39 | 5.2:1 | 3.06:1 | 0% | 16.0+38.2+61.2 = 115.4 |
| 5 | scallion (first to cut) | E3-r8-05 | 36 | 5.21:1 | 3.07:1 | 0% | 15.8+37.8+61.6 = 115.2 |

Native weight: 580.1 KB for all 5 (on top of the base), 464.9 KB without scallion. Web loads one file only on an egg
day (16 / 38 / 62 KB by screen density). Medium only: the one faint/medium pair (E3-r7-01f / 01m) is in the gallery.
Score trend (best per round, self, /50): r4 38 -> r5 39 -> r6 39 -> r7 40 -> r8 40; the set's weakest went from
33 (thyme, r6) to 36. The outside panel ran about 1 point per lens lower than these self-grades on round 6.

## Files

- `gallery.html` (phone, self-contained): base, the 5 finals (island iPhone 393, notch iPhone 390, phone web 390 and
  320, a 3x close-up of the phone hero, iPad 820, 1280 at true 1x), the faint/medium pair, how often, then EVERY egg
  from every round (E3 rounds 7, 6, 5, 4; lanes E1 and E2 rounds 1-3), each re-shot on the agreed bar on the island
  iPhone, with its id, what it tries, grade and verdict.
- `desktop.html`: base + the 5 finals LIVE at 1280, 820, 1180, 1920 (tiles embedded once; 1x/2x by screen).
- `SCHEDULE.md` + `schedule.json`: the egg-day function, re-run for 5 eggs (and 4).
- `STATE.md`: the short state. `tiles/`: every egg `@1x/@2x/@3x.webp` (1440x140 CSS). `results.json`: per tile
  weights, file check, shot contrast and "food behind words" per width.
- `gen/`: `egg7.py` (rounds 7-8 generator: keep-out map, new shapes, hero spots, mid group, sprinkle), `egg.py`
  (rounds 4-6, unchanged), `eggs_r7.py`, `eggs_r8.py` (recipes), `mock.py` (now draws the Dynamic Island and the
  notch with clock, signal, wifi, battery), `shoot.py` (11 widths; the 'fit' narrow rule; behind-words check),
  `old_shots.py`, `build_pages.py`, `tables.py`, `schedule.py`, `grades.py`. Shots: scratch `.../i007/shots_E4/`.

## Rounds 7-8: what each round-6 panel finding became

1. **Medium only; thyme + pepper cut.** Round 7 makes medium only plus one faint twin (chives) for Tyler.
2. **Island / notch.** `mock.py` draws the Dynamic Island (393: x 125-268, y 11-48, 59 inset, clock and icons in the
   ears) and the notch (390: x 110-280, 32 tall, 47 inset). Phones are shot both ways. Strip bits now sit only between
   the clock and the cut-out (x 86-108) or in the strip just under the cut-out (tile y 75-83), never behind it.
3. **No food behind words, a hero that moves, diffuse on phone, a mid-bar group.** `egg7.py` builds a keep-out map of
   every word and cut-out at every phone, iPad and web width (name + mark, "Saved"/cloud, timer + count, account,
   phone clock/signal/battery, island, notch, iPad clock/battery), and tests each bit's real drawn shape against it.
   The row's top strip (tile y 84-98) and bottom strip (126-139) hold no glyph at any width, so the phone hero lives
   there, right of the name: clear of "Saved" at 320/360/375/390 (shot at each). Each egg has its own hero spot
   (top or bottom strip, its own x range, angle and spread). 4-5 faint bits are spread across the phone row; wide
   bars get a second group at hero strength mid-bar (tile x 478-588, free of words at every width). Round 8 also
   keeps every field bit out of the wide-bar word zones. Measured: food behind words = 0.0% at all 11 widths for
   every final (pixels changed by more than 30 levels vs the base inside the word boxes; WebP noise alone is ~27).
4. **White onion.** Built layer by layer: uneven thickness and length, a small core so a slice is a solid half-moon
   (not a fan of arcs), one layer often slipped out (moved and turned), warm yellow-ivory, a thin bright rim. Round 8
   darkens the body a little so the rims read bright, makes the slices bigger and moves the hero slice to the top strip.
5. **Red onion.** Pieces placed 9-16 px apart, a deep purple skin edge (#5C1A4E), loose layers 1.25x thicker.
6. **Parsley.** A faint pale midrib to each lobe, a short paler stem, a lighter lit edge (rim 0.62), a brighter green.
   Round 8 makes its phone hero fuller (4 leaves + 4 bits, low strip).
7. **Chives.** Three greens (dark, mid, light) and a few tubes cut on a slant (pale cut wall, dark hollow).
8. **Scallion, one try.** Open rings: the wood shows through the middle, a thin wall, tilted ovals, often a partial
   inner layer. Round 7's rings touched and looked like chain links; round 8 spaces them so none touch and thickens the
   wall. Verdict: reads as rings, not peas; kept as the 5th egg and named the first to cut.

## Round 7 (6): what I saw

- First try put the phone hero in the thin strips at its old size: clear of every word but too quiet. Rebuilt as a
  pile of 6-8 bigger bits (1.15-1.22x) in one strip plus 2-3 bits in the other. Then: chives and red onion read at a
  glance on a phone; parsley's hero was too small; white onion now a solid uneven half-moon, still tan; scallion rings
  touched (chain links). Faint twin: the pile is easy to miss.
Best: E3-r7-01m (40), r7-03m (39).

## Round 8 (5): what I saw

- Chives: unchanged hero, fuller mid group; the cleanest egg. Parsley: the fuller low pile reads as leaves on a phone.
  Red onion: purple skin lines, pieces apart; the clearest onion. Chives + onion: the big top-strip half-moon is
  clearly an onion SHAPE at 2x-3x, but the colour is still tan-ivory (the cap). Scallion: separate open rings.
- On iPad 820 and 1280 every egg shows three places (phone hero, mid group, field) and stays light.
Best: E3-r8-01 (40).

## Still weak (say it plainly)

- White onion is still tan, not white. Every pixel must stay at or under the lightest wood (5.15:1 for cream text),
  so nothing on the bar can ever be white. It reads as onion by its layered half-moon shape and next to the chives.
- All five are calmer than the old website's eggs (that one used bright green and red at 0.85-0.95).
- Scallion could still pass for little O-rings to some people; it is the first to cut.
- On a 1x desktop the eggs are "look for it" (the mid group helps). Seen only in browser mocks, not on a real
  iPhone/iPad (island, low screen brightness).
- Self-grades only for rounds 7-8; no outside panel on them yet.

# Rounds 4-6 (archive)

### How an egg is made (and what each panel finding became)

1. **Style (finding: E2 drawing + E1 layout).** Each bit is drawn with lane E2's renderer: a solid shape from a
   distance field, a dome normal, one lit side (top left), a soft contact shadow down-right, plus a soft damp rim
   around each bit (new; it makes pale bits stand off the wood). Layout is lane E1's idea: a faint even field plus
   3-4 loose knife-sweep groups (rotated soft ellipses) spread along the bar, one in the first third of a wide bar.
   No hollow outline rings anywhere: chive ends are solid coins, scallion slices are filled.
2. **Contrast (finding: cap every pixel).** Glints are added BEFORE the cap; then every pixel is capped (soft knee,
   hard ceiling) so cream #FAF4EB is 5.15:1 or better; each WebP is decoded and fixed where the encoder lifted a
   pixel (lane N's `encode_safe`, whole tile, no exception zone). `shoot.py` then re-checks every decoded file at
   1x/2x/3x for every width 320-2560, bottom-anchored (phone 103, iPad 80, web 56 tall): worst of all 35 tiles
   **5.15:1** (base 5.17). So every word zone passes (name, mark, status slot, "Saved", timer count, account, phone
   clock and battery), and the saving cloud gold #E2B86A is **3.03:1 or better on any pixel**.
3. **Onion (finding: shape, not whiteness).** Half-moon slices (6-9 px, 2-4 nested layers, a see-through gap between
   layers, a bright rim on each layer's outer edge) and loose crescents (one curved layer, 10-20 px long, bright outer
   rim, tapered tips): 2-3x the old dice. Warm ivory #F8E6BE body, see-through, no grey mute. Red onion: the same
   shapes with purple #86306A layer edges. What I saw: the SHAPE now says onion at 3x and on a phone at 2x; the white
   onion still reads pale taupe, not white (the cap keeps any bit at or under the lightest wood); red onion reads best.
4. **Variety (finding: differ by shape and layout).** Finals are six shapes: green rods (chives), pale half-moons +
   rods (chives + onion), purple arcs (red onion), whole leaves (parsley), sprigs + specks (thyme + pepper), green
   discs (scallion). Cut on the way: fine chives (a weaker batons), onion alone (too pale to carry an egg), both onion
   shapes at once (busy), mixed herbs, cilantro, red onion + parsley, cilantro + red onion (kept as spares). Never
   made: flour, autumn, grime-like pepper, gremolata.
5. **Noticeable but light (finding: hero + faint field; faint / medium).** One hero group of 3-6 crisper, slightly
   bigger bits right of the name inside the bottom 56 (tile x 192-246, y 96-130): left of "Saved" on a 390 phone, so
   phone web sees it, and the first third of every wide bar. Faint = field opacity 0.6, hero 0.82, 0.8x the field bits;
   medium = field 0.95, hero 1.0, 1.3x the field bits, hero 1.15x size.
6. **Phone (finding: status strip; shoot with and without).** 2-3 bits in the status strip between the clock (x < 100)
   and the battery (x 255-410). Every egg is shot at 390 with the status bar (app) and without (phone web).
7. **Agreed bar only.** Board N-r8-01, Fraunces SemiBold Italic 24 name (lane N font), the true app-icon tile
   (`favicon-tile.svg` from `origin/main`, byte-identical to lane N's), mark inset 16 phone / 22 wide, "Saved" + timer
   count 2 + account. Name ends at x 167 (phone) / 173 (wide); no bit in the row left of x 172.
8. **Schedule:** `SCHEDULE.md`. 9. **Weight:** every tile 112.8-117.0 KB for 1x+2x+3x (budget 130).

### How it was judged

- Grades 1-10, strict (self-grades run about 1 high): **B**eauty, **F** believable food, **L**ight (does not
  obscure), **R**eadability (words + worst contrast), **N**oticeable (on a phone, at a glance).
- Looked at, for every round: the 390 phone sheet (with and without status bar) at 2x, 1280 at true 1x, 820, and the
  3x file 1:1 around the hero (x 160-460); species specimen sheets at 3x and 1x before each round.
- Contrast: the file check above (every pixel, every width) and the 7 shot widths with words hidden (whole bar).

### Round 4 (13): what I saw

- The hero group works: on a phone the eye lands on 3-6 bits right of "Craft"; the rest is a faint field and a few
  bits by the clock. On 1280 at 1x the bar reads as wood first, food second.
- Chive batons (r4-01) read at every size. Red onion (r4-06, 07) is the clearest onion. Whole parsley leaves (r4-10)
  read as leaves: a truly new shape. Half-moons (r4-03) show nested layers, but are pale taupe.
- Misses: scallion slices read as peas (r4-08); thyme + pepper is nearly invisible (r4-12); chive coins read as dots.
Best: E3-r4-01, r4-06, r4-07 (38).

### Round 5 (10): changes and what I saw

Changes: half-moons 6-9 px with more layers and a deeper shadow; scallion bigger and flatter; batons straighter; a new
thyme sprig (stem + leaf pairs); field a little fuller. Saw: chives + half-moons now look like Tyler's sentence; onion
alone too pale to carry an egg (cut); scallion shows a ring at 3x but still peas at 1x; thyme sprigs read up close but
are dark on brown. Best: E3-r5-01 (39), r5-04, r5-05, r5-07 (38).

### Round 6 (6 finals x faint / medium): changes and what I saw

Changes: white onion glassier (see-through flesh, bright rim per layer); scallion with a dark wall, a pale ring and a
dark hollow core; thyme lighter grey-green, bigger sprigs; faint / medium differ in opacity AND count AND hero size
(the first try, opacity only, looked the same on a phone). Saw: faint is a "you have to look" egg, medium is a
"someone was cooking" egg; both keep the name, status and account clear. Thyme + pepper stays the quietest.

Score trend (best per round, self, /50): r4 38 -> r5 39 -> r6 39. (Lanes E1/E2 self-graded their r3 at 41; the panel
put them at 6-7 per lens, about 33-35 on this scale.)

### The 6 finals

| # | egg | faint id: sum | medium id: sum | worst (f / m) | KB (f / m) |
|---|---|---|---|---|---|
| 1 | chive batons | E3-r6-01f: 39 | E3-r6-01m: 39 | 5.21 / 5.20 | 115.0 / 116.9 |
| 2 | chives + white onion half-moons | E3-r6-02f: 36 | E3-r6-02m: 38 | 5.19 / 5.15 | 113.0 / 116.1 |
| 3 | red onion | E3-r6-03f: 37 | E3-r6-03m: 38 | 5.20 / 5.16 | 112.8 / 115.5 |
| 4 | parsley leaves | E3-r6-04f: 38 | E3-r6-04m: 38 | 5.21 / 5.21 | 114.6 / 116.7 |
| 5 | thyme sprigs + cracked pepper | E3-r6-05f: 33 | E3-r6-05m: 35 | 5.21 / 5.15 | 115.2 / 115.4 |
| 6 | scallion slices | E3-r6-06f: 35 | E3-r6-06m: 36 | 5.16 / 5.19 | 115.3 / 116.1 |

Shipped set (medium, 6 eggs): **697 KB** native (116.9 + 116.1 + 115.5 + 116.7 + 115.4 + 116.1, on top of the
115 KB base); faint set 686 KB; 5 medium eggs (drop thyme) 581 KB. Web loads one file only on an egg day (15-16 / 38 / 62 KB by density).
My pick: **medium**, five eggs (1-4 + 6), thyme + pepper as a spare. Faint is right only if Tyler wants it truly hidden.

### Still weak

- White onion is pale taupe, not white: the 5.15 cap keeps every bit at or under the lightest wood. It reads as onion
  by its layered half-moon shape and next to the chives; alone it would not. Red onion is the stronger onion.
- Scallion slices can still pass for peas at 1x on a phone; the ring shows at 2x-3x.
- Thyme + pepper is the quietest egg; on a 1x desktop you must look for it.
- Faint eggs on a phone show mostly the hero group; most of the phone row is bare (the status-slot and account
  dips). That is by design ("very light"), but faint may go unnoticed on a rare egg day.
- Self-grades only; no outside panel on rounds 4-6 yet. Seen only in a browser mock, not on a real iPhone/iPad.

## Score tables (all rounds; contrast and "behind words" re-measured on the round-7 mock)

### Round 4

| id | from | what it tries | B | F | L | R | N | sum | worst, every pixel 1x/2x/3x, widths 320-2560 | shot worst (11 widths, whole bar) | gold on worst | food behind words, max % (11 widths) | bits (hero) | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E3-r4-01 | E2-r3-01 x E1-r3-01 | chive batons: long rods in loose knife sweeps | 7 | 7 | 8 | 9 | 7 | 38 | 5.23 / 5.21 / 5.21 | 5.21 | 3.07 | 0.35 | 78 (5) | 15.8+38.4+61.3 = 115.5 | keep: batons read as chives at every size; the heap right of the name is the hero. |
| E3-r4-02 | E2-r3-01 x E1-r3-05 | chives cut fine: short rods + solid coins (no hollow rings) | 6 | 6 | 8 | 9 | 5 | 34 | 5.21 / 5.21 / 5.19 | 5.22 | 3.05 | 0.32 | 104 (5) | 15.8+38.3+62.1 = 116.2 | cut: fine chives are a weaker r4-01; end-on coins read as dark dots. |
| E3-r4-03 | E1-r3-06 x E2-r3-02 | onion half-moons alone: nested layer arcs, bright rims | 6 | 6 | 8 | 9 | 6 | 35 | 5.21 / 5.19 / 5.17 | 5.19 | 3.04 | 0.94 | 26 (2) | 15.7+37.8+60.2 = 113.7 | keep: half-moons show nested layers (onion SHAPE); still pale taupe, not white. |
| E3-r4-04 | E1-r3-02 | chives + onion crescents (loose single layers) | 6 | 6 | 8 | 9 | 6 | 35 | 5.21 / 5.18 / 5.18 | 5.18 | 3.05 | 0.67 | 84 (5) | 15.9+38.3+62.8 = 117.0 | merge: crescents alone look like pale C marks; pair half-moons with chives. |
| E3-r4-05 | E1-r3-02 x E2-r3-02 | chives + onion, both shapes (half-moons and crescents) | 6 | 6 | 7 | 9 | 6 | 34 | 5.18 / 5.15 / 5.21 | 5.15 | 3.03 | 1.05 | 86 (4) | 15.9+38.6+62.1 = 116.6 | cut: both onion shapes + chives is busy. |
| E3-r4-06 | E2-r1-08 | red onion half-moons + crescents (purple layer edges) | 7 | 7 | 8 | 9 | 7 | 38 | 5.2 / 5.21 / 5.21 | 5.2 | 3.06 | 1.06 | 29 (3) | 15.4+37.8+60.9 = 114.1 | keep: purple layer edges make red onion the clearest onion. |
| E3-r4-07 | E2-r1-08 | red onion + flat parsley leaves | 7 | 7 | 8 | 9 | 7 | 38 | 5.18 / 5.15 / 5.24 | 5.2 | 3.03 | 1.16 | 61 (4) | 15.6+37.8+61.4 = 114.8 | keep: red onion + parsley leaves, a nice pair. |
| E3-r4-08 | E1-r3-08 | scallion slices, solid (green and pale), no washers | 5 | 4 | 8 | 9 | 6 | 32 | 5.21 / 5.21 / 5.22 | 5.21 | 3.07 | 0.99 | 63 (5) | 16.0+38.3+61.7 = 116.0 | fix: scallion slices read as peas; need a visible ring and core. |
| E3-r4-09 | E1-r3-08 x E2-r3-01 | scallion slices + chive batons (stir-fry) | 5 | 5 | 8 | 9 | 6 | 33 | 5.15 / 5.16 / 5.2 | 5.15 | 3.03 | 1.12 | 62 (4) | 15.9+38.0+62.6 = 116.5 | merge into the scallion rebuild. |
| E3-r4-10 | E1-r3-03 x E2-r3-03 | whole flat-leaf parsley leaves, a few chopped bits | 7 | 7 | 8 | 9 | 6 | 37 | 5.21 / 5.21 / 5.16 | 5.21 | 3.04 | 0.28 | 69 (3) | 15.6+38.2+62.0 = 115.8 | keep: whole parsley leaves read as leaves, a new shape. |
| E3-r4-11 | E1-r3-03 | mixed herbs: parsley leaves, chive rods, thyme | 6 | 6 | 8 | 9 | 5 | 34 | 5.18 / 5.21 / 5.17 | 5.18 | 3.04 | 0.35 | 104 (6) | 15.7+37.9+61.9 = 115.5 | spare: mixed herbs fine but looks like parsley + chives, nothing new. |
| E3-r4-12 | E1-r3-04 x E2-r3-05 | thyme + cracked pepper (small, a few whole corns) | 5 | 5 | 9 | 9 | 3 | 31 | 5.2 / 5.23 / 5.2 | 5.2 | 3.06 | 0.12 | 154 (7) | 15.3+37.6+61.5 = 114.4 | fix: thyme + pepper almost invisible on a phone. |
| E3-r4-13 | E2-r3-08 | cilantro leaves, round lobes | 6 | 6 | 8 | 9 | 6 | 35 | 5.23 / 5.21 / 5.2 | 5.21 | 3.06 | 0.2 | 61 (3) | 15.7+37.9+62.3 = 115.9 | keep: cilantro leaves read; a softer parsley. |

### Round 5

| id | from | what it tries | B | F | L | R | N | sum | worst, every pixel 1x/2x/3x, widths 320-2560 | shot worst (11 widths, whole bar) | gold on worst | food behind words, max % (11 widths) | bits (hero) | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E3-r5-01 | E3-r4-01 | chive batons: straight long rods in loose sweeps, a small heap by the name | 7 | 8 | 8 | 9 | 7 | 39 | 5.2 / 5.21 / 5.16 | 5.16 | 3.04 | 0.88 | 78 (5) | 15.6+38.4+62.5 = 116.5 | final: straight batons, the cleanest egg. |
| E3-r5-02 | E3-r4-04 x E3-r4-03 | chives + onion half-moons | 7 | 6 | 8 | 9 | 7 | 37 | 5.22 / 5.16 / 5.21 | 5.16 | 3.04 | 0.32 | 74 (4) | 15.9+38.4+62.6 = 116.9 | final: chives + bigger half-moons; Tyler's own words. |
| E3-r5-03 | E3-r4-03 | onion alone: half-moons and loose layers | 6 | 6 | 8 | 9 | 6 | 35 | 5.22 / 5.21 / 5.21 | 5.22 | 3.07 | 0.44 | 37 (3) | 15.9+37.4+60.2 = 113.5 | cut: onion alone is too pale to carry an egg; it needs the chives. |
| E3-r5-04 | E3-r4-06 | red onion: half-moons and loose layers, purple edges | 7 | 7 | 8 | 9 | 7 | 38 | 5.21 / 5.21 / 5.2 | 5.21 | 3.06 | 0.99 | 33 (3) | 15.8+38.0+60.5 = 114.3 | final: red onion, purple arcs. |
| E3-r5-05 | E3-r4-07 | red onion + flat parsley leaves | 7 | 7 | 8 | 9 | 7 | 38 | 5.23 / 5.21 / 5.21 | 5.21 | 3.07 | 0.85 | 54 (4) | 15.6+38.2+61.7 = 115.5 | spare: red onion + parsley (too close to the two finals it mixes). |
| E3-r5-06 | E3-r4-08 x E3-r4-09 | scallion slices (bigger, layer lines) + a few chive batons | 6 | 5 | 8 | 9 | 7 | 35 | 5.23 / 5.16 / 5.21 | 5.16 | 3.04 | 0.09 | 57 (4) | 16.1+38.0+62.4 = 116.5 | fix: bigger slices show a ring at 3x, still peas at 1x; darker wall next. |
| E3-r5-07 | E3-r4-10 | whole flat-leaf parsley leaves | 7 | 7 | 8 | 9 | 7 | 38 | 5.21 / 5.2 / 5.21 | 5.21 | 3.06 | 0.78 | 61 (3) | 15.9+37.9+60.9 = 114.7 | final: parsley leaves. |
| E3-r5-08 | E3-r4-11 | mixed herbs: parsley leaves, chive rods, thyme sprigs | 6 | 6 | 8 | 9 | 6 | 35 | 5.22 / 5.2 / 5.2 | 5.2 | 3.06 | 0.83 | 76 (4) | 15.6+38.2+62.4 = 116.2 | spare: mixed herbs with thyme sprigs. |
| E3-r5-09 | E3-r4-12 | thyme sprigs + cracked pepper (small), a few whole corns | 6 | 6 | 9 | 9 | 4 | 34 | 5.21 / 5.24 / 5.2 | 5.21 | 3.06 | 0.06 | 118 (6) | 15.4+37.5+61.4 = 114.3 | fix: sprigs read as sprigs up close; too dark to notice; lighten. |
| E3-r5-10 | E3-r4-13 x E3-r4-06 | cilantro leaves + red onion crescents | 7 | 6 | 8 | 9 | 7 | 37 | 5.22 / 5.2 / 5.16 | 5.2 | 3.04 | 0.61 | 46 (4) | 15.8+37.9+61.5 = 115.2 | spare: cilantro + red onion (taco night, only visible parts named). |

### Round 6

| id | from | what it tries | B | F | L | R | N | sum | worst, every pixel 1x/2x/3x, widths 320-2560 | shot worst (11 widths, whole bar) | gold on worst | food behind words, max % (11 widths) | bits (hero) | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E3-r6-01f | E3-r5-01 | chive batons: straight rods in loose sweeps, a small heap by the name (faint) | 7 | 8 | 9 | 9 | 6 | 39 | 5.22 / 5.23 / 5.21 | 5.22 | 3.07 | 0.37 | 64 (5) | 15.5+37.8+61.7 = 115.0 | chives, faint: a quiet heap by the name, light flecks elsewhere. |
| E3-r6-01m | E3-r5-01 | chive batons: straight rods in loose sweeps, a small heap by the name (medium) | 7 | 8 | 8 | 9 | 7 | 39 | 5.21 / 5.2 / 5.2 | 5.2 | 3.06 | 0.87 | 99 (5) | 16.1+38.9+61.9 = 116.9 | chives, medium: the egg most people will spot and name. |
| E3-r6-02f | E3-r5-02 | chives + white onion half-moons (Tyler's own words) (faint) | 7 | 6 | 9 | 9 | 5 | 36 | 5.2 / 5.19 / 5.19 | 5.19 | 3.05 | 0.5 | 60 (4) | 15.6+37.7+59.7 = 113.0 | chives + onion, faint: onion half-moons get lost. |
| E3-r6-02m | E3-r5-02 | chives + white onion half-moons (Tyler's own words) (medium) | 7 | 7 | 8 | 9 | 7 | 38 | 5.15 / 5.21 / 5.21 | 5.15 | 3.03 | 1.44 | 93 (4) | 16.3+37.9+61.9 = 116.1 | chives + onion, medium: half-moons read as sliced onion next to chives. |
| E3-r6-03f | E3-r5-04 | red onion: half-moons and loose layers, purple edges (faint) | 7 | 7 | 9 | 9 | 5 | 37 | 5.22 / 5.23 / 5.2 | 5.23 | 3.06 | 1.23 | 27 (3) | 15.4+37.7+59.7 = 112.8 | red onion, faint: purple arcs, easy to miss. |
| E3-r6-03m | E3-r5-04 | red onion: half-moons and loose layers, purple edges (medium) | 7 | 7 | 8 | 9 | 7 | 38 | 5.23 / 5.16 / 5.21 | 5.16 | 3.04 | 2.21 | 41 (3) | 16.0+38.1+61.4 = 115.5 | red onion, medium: clearest onion of all. |
| E3-r6-04f | E3-r5-07 | whole flat-leaf parsley leaves, a few chopped bits (faint) | 7 | 7 | 9 | 9 | 6 | 38 | 5.21 / 5.21 / 5.21 | 5.21 | 3.07 | 0.57 | 50 (3) | 15.4+37.6+61.6 = 114.6 | parsley leaves, faint. |
| E3-r6-04m | E3-r5-07 | whole flat-leaf parsley leaves, a few chopped bits (medium) | 7 | 7 | 8 | 9 | 7 | 38 | 5.21 / 5.21 / 5.22 | 5.21 | 3.07 | 0.79 | 78 (3) | 15.9+38.1+62.7 = 116.7 | parsley leaves, medium: leaf shapes clear on a phone. |
| E3-r6-05f | E3-r5-09 | thyme sprigs + cracked pepper (small), a few whole corns (faint) | 6 | 6 | 9 | 9 | 3 | 33 | 5.21 / 5.21 / 5.21 | 5.21 | 3.07 | 0.15 | 91 (6) | 15.6+37.9+61.7 = 115.2 | thyme + pepper, faint: nearly invisible; only for people who look. |
| E3-r6-05m | E3-r5-09 | thyme sprigs + cracked pepper (small), a few whole corns (medium) | 6 | 6 | 9 | 9 | 5 | 35 | 5.16 / 5.17 / 5.15 | 5.16 | 3.03 | 0.18 | 143 (6) | 15.5+38.2+61.7 = 115.4 | thyme + pepper, medium: sprigs show; still the quietest final. |
| E3-r6-06f | E3-r5-06 | scallion slices (dark wall, pale ring, hollow core) + a few chive batons (faint) | 6 | 6 | 8 | 9 | 6 | 35 | 5.16 / 5.21 / 5.2 | 5.2 | 3.04 | 0.58 | 43 (4) | 15.7+37.7+61.9 = 115.3 | scallion, faint: green slices, ring visible up close. |
| E3-r6-06m | E3-r5-06 | scallion slices (dark wall, pale ring, hollow core) + a few chive batons (medium) | 6 | 6 | 8 | 9 | 7 | 36 | 5.2 / 5.21 / 5.19 | 5.2 | 3.05 | 0.9 | 66 (4) | 16.2+38.2+61.7 = 116.1 | scallion, medium: noticeable; at 1x could still pass for peas. |

### Round 7

| id | from | what it tries | B | F | L | R | N | sum | worst, every pixel 1x/2x/3x, widths 320-2560 | shot worst (11 widths, whole bar) | gold on worst | food behind words, max % (11 widths) | bits (hero) | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E3-r7-01m | E3-r6-01m | chive batons in three greens + a few slant-cut tubes; a pile along the top of the row, two rods low | 7 | 8 | 8 | 9 | 8 | 40 | 5.23 / 5.21 / 5.21 | 5.21 | 3.07 | 0.22 | 101 (15) | 16.1+38.7+62.2 = 117.0 | chives: a pile along the top of the row reads at a glance; three greens + slant cuts; clear of every word. |
| E3-r7-01f | E3-r6-01f | chive batons in three greens + a few slant-cut tubes; a pile along the top of the row, two rods low (faint twin, for comparison) | 7 | 8 | 9 | 9 | 6 | 39 | 5.2 / 5.2 / 5.21 | 5.2 | 3.06 | 0.0 | 71 (15) | 15.7+38.1+62.5 = 116.3 | chives, faint twin: same layout; the pile is easy to miss on a phone. Kept only for the faint/medium compare. |
| E3-r7-02m | E3-r6-02m | chives + white onion: uneven layers (one slipped out), yellow-ivory, a thin bright rim | 6 | 6 | 8 | 9 | 7 | 36 | 5.21 / 5.15 / 5.21 | 5.19 | 3.03 | 0.82 | 94 (13) | 16.1+38.8+61.7 = 116.6 | chives + onion: solid half-moons with a slipped layer (no more fans), but still tan, and the hero slice is cut by the bar bottom. |
| E3-r7-03m | E3-r6-03m | red onion: pieces kept apart, a deeper purple skin edge, thicker loose layers; hero up top | 7 | 7 | 8 | 9 | 8 | 39 | 5.21 / 5.2 / 5.22 | 5.2 | 3.06 | 1.53 | 50 (10) | 15.9+38.2+59.7 = 113.8 | red onion: pieces apart, purple skin lines clear; the hero up top reads as onion on a phone. |
| E3-r7-04m | E3-r6-04m | parsley leaves with a faint midrib and short stem, a lighter lit edge, a little brighter green | 7 | 7 | 8 | 9 | 6 | 37 | 5.21 / 5.2 / 5.21 | 5.2 | 3.06 | 0.98 | 87 (12) | 16.0+38.7+63.2 = 117.9 | parsley: midrib + stem show at 3x, a little brighter; the hero is too small on a phone. |
| E3-r7-05m | E3-r6-06m | scallion, one more try: open rings that show the wood, thin walls, tilted ovals | 5 | 5 | 8 | 9 | 6 | 33 | 5.21 / 5.21 / 5.18 | 5.21 | 3.05 | 0.25 | 69 (12) | 15.9+38.4+61.3 = 115.6 | scallion: open rings no longer read as peas, but touching rings look like chain links or O-rings. |

### Round 8

| id | from | what it tries | B | F | L | R | N | sum | worst, every pixel 1x/2x/3x, widths 320-2560 | shot worst (11 widths, whole bar) | gold on worst | food behind words, max % (11 widths) | bits (hero) | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E3-r8-01 | E3-r7-01m | chive batons in three greens + slant-cut tubes; a pile along the top of the row, two rods low | 7 | 8 | 8 | 9 | 8 | 40 | 5.17 / 5.21 / 5.16 | 5.17 | 3.04 | 0.0 | 103 (17) | 16.2+38.8+62.2 = 117.2 | FINAL 1. Chives: the cleanest egg; a pile along the top of the row on a phone, a fuller group mid-bar on wide bars. |
| E3-r8-02 | E3-r7-02m | chives + white onion: big uneven half-moons (one layer slipped), bright rims on a darker body; hero up top | 6 | 6 | 8 | 9 | 7 | 36 | 5.21 / 5.18 / 5.2 | 5.18 | 3.05 | 0.0 | 95 (15) | 16.1+37.8+61.3 = 115.2 | FINAL 3. Chives + white onion (Tyler named it): big uneven half-moons up top; shape says onion, colour still tan. |
| E3-r8-03 | E3-r7-03m | red onion: pieces kept apart, a deep purple skin edge, thick loose layers; hero up top | 7 | 7 | 8 | 9 | 8 | 39 | 5.2 / 5.21 / 5.21 | 5.2 | 3.06 | 0.0 | 52 (12) | 16.0+38.2+61.2 = 115.4 | FINAL 4. Red onion: purple skin lines, pieces apart; the clearest onion. |
| E3-r8-04 | E3-r7-04m | parsley leaves with a faint midrib and short stem, a lighter lit edge; a fuller hero low in the row | 7 | 7 | 8 | 9 | 7 | 38 | 5.21 / 5.2 / 5.2 | 5.2 | 3.06 | 0.0 | 92 (17) | 16.1+38.7+62.3 = 117.1 | FINAL 2. Parsley: leaves with a midrib and stem, a fuller hero low in the row. |
| E3-r8-05 | E3-r7-05m | scallion: open rings with a thicker wall and an inner layer, spaced so no two touch | 6 | 6 | 8 | 9 | 7 | 36 | 5.21 / 5.21 / 5.21 | 5.21 | 3.07 | 0.0 | 65 (13) | 15.8+37.8+61.6 = 115.2 | FINAL 5 (first to cut). Scallion: open rings, spaced apart; reads as rings, not peas; could pass for little O-rings. |

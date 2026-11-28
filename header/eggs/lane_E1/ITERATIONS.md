# I-007 part E, lane E1: header-board Easter eggs, rounds 1-3

2026-11-27. 32 eggs in 3 rounds (14, 10, 8 finals), each the agreed board N-r8-01 with a very light scatter of chopped
food baked in. Drawn style: flat, hand-cut vector bits, softened and laid on at low opacity with a faint contact shadow.
How the old site did it, and the "how often" proposal: `OLD_SITE.md`.

Files: `gallery.html` (phone, self-contained: proposal, base board, top 3, other finals, rounds 2 and 1), `desktop.html`
(base + top 3 at 1280, 820, 1180), `tiles/` (every egg `@1x/@2x/@3x.webp`, plus `N-r8-01` copied from lane N),
`results.json` (tile meta + every contrast number), `gen/` (recipes), `OLD_SITE.md`.
Recipes: `gen/egg.py` (re-renders N-r8-01 with lane N's own `board_n.py`, draws the bits, caps, encodes, checks),
`gen/eggs.py` + `eggs_r2.py` + `eggs_r3.py` (the eggs), `gen/make.py r3` (tiles), `gen/shoot.py r3 --base` (shots +
contrast + sheets), `gen/grades.py`, `gen/build_pages.py`. Bar: lane N's `mock.py`, copied unchanged (Fraunces 22
name, true icon tile, 56 row, 1 px rule). Shots: scratch `.../scratchpad/i007/shots_E1/`.

## How it was made

- The base is not re-encoded from the WebP: `egg.py` re-renders N-r8-01 from its recipe (lane N `R8`, seed 504) in
  linear light at 3x (matches lane N's 3x file to WebP noise: mean 3.3/255), paints the bits on that, then runs lane N's
  own `finish` (the soft luminance cap) and `encode_safe` (decode every file, darken only the pixels WebP lifted).
  So every pixel of every egg file gives cream `#FAF4EB` **5.15:1 or better**, anywhere on the tile, at 1x, 2x, 3x.
  That covers every screen width and every word (name, mark, account, timer, "Sign in", the phone's clock), not only
  the widths shot. One file (r1-02 @2x) stuck at 4.81 after 24 tries; `save_egg` now retries at slightly higher
  quality, and it passed at 5.21.
- Bits are drawn at 12 px per CSS px, blurred 0.1 CSS px, shrunk to 3x, laid on in linear light; each bit gets a
  random "depth" (0.65-1.1 of its opacity) so some sit deeper in the picture. Bits that cross a tile edge are drawn on
  both sides (indices wrap), so the tile still repeats with no seam.
- Where bits go (round 2+): the bar row keeps the mark + name clear (x < 185), a light fringe to 250, full from 330;
  the strip above the row (only phones and iPads show it, as the status bar) keeps only the clock clear (x < 85);
  a soft dip at the account spot of 390 / 820 / 1180 / 1280 / 1440 / 1920 screens; a slight lean toward the bottom
  (web shows only the bottom 56 of the 140 tile). Most eggs add one soft "sweep" where a phone sees it.
- Strength (opacity scale) 1.8 in rounds 1-2, 2.0 in the finals.

## How it was judged

- Grades 1-10, strict (self-grades run about 1 high): **B**eauty, **F**ood believable, **L**ightness (does not
  obscure), **R**eadability (worst contrast), **T** fit with the board and the app.
- Contrast: each width shot again with words, mark, avatar and status text hidden; cream against the single lightest
  pixel in each box. Widths: 390 (status 47, 3x), 820 and 1180 (iPad, status 24, 2x), 1280 (2x), 1280 and 1920 (1x).
  "Phone clock" = the 390/820/1180 status-bar time and battery boxes.
- Looked at: the 390 sheets at 2x, the 1280 sheets at true 1x, the 3x file at 1:1 (CSS x 380-800) and zoomed 2x.

## Round 1 (14 eggs)

What I saw:
- Chive rings read as rings at 3x once they got bigger (about 1.4x life size: a 3-4 mm chive is only 3 CSS px on a
  36 px block) and an open hollow with a dark inner edge. At true size they started as invisible smudges; the first
  try was too faint and too small.
- Knife "sweeps" (r1-02: a few soft clusters on a thin field) look like real prep; an even spread reads a little like
  confetti (r1-05).
- White and pale bits go grey on orange wood (onion r1-03, garlic, salt): the contrast cap keeps them dark, and next to
  saturated wood any pale, unsaturated patch looks grey-pink. Scallion (r1-08) read as round water spots.
- Knife marks (the old site's 15 in 100) cannot be seen at this weight: cut. Dill reads as squiggles: cut.
- **The big miss:** the round-1 keep-clear rule (every row clear up to x 330) left the phone bar almost empty, and the
  phone is where the bar is seen most.
Best: **E1-r1-02** (39), **E1-r1-01** (39), E1-r1-09 (38).

Changes for round 2: a 2-D keep-clear zone (the status strip can hold bits beside the clock), a sweep where a phone
sees it; onion yellower, crisper, with a bright skin line and a wet glint; scallion as crisp rings (no disc); thyme a
size up; salt and knife marks dropped; one stronger test (r2-10).

## Round 2 (10 eggs)

What I saw:
- The phone now shows the egg: a few chive rings beside the clock and right of the name, the name itself clear.
- Onion reads warm and see-through now (r2-03, r2-05); alone it could pass for garlic, so it gets a few chives.
- Strength 2.3 (r2-10) is still light at 1x but busier at 3x: the finals use 2.0.
- Scallion (r2-08) still grey discs: rebuilt like the chive ring for round 3. Pasta night (r2-09) too sparse and the
  chili too faint (the cap mutes red): cut.
Best: **E1-r2-01** (41), **E1-r2-04** (41), **E1-r2-02** (41), E1-r2-03 (40).

## Round 3 (8 finals)

What I saw:
- The chive eggs are the strongest: at 3x they look like a board someone just chopped chives on; at 1x and on a phone
  they are a faint green fleck in the wood, nothing more.
- Chives + onion (r3-02) is Tyler's own sentence in one picture.
- Scallion (r3-08) finally reads as slices; the white slices are still a little cool.
- Score trend (best per round, self, /50): r1 39 → r2 41 → r3 41 (three finals at 41).

## Top 3

1. **E1-r3-02** chives + diced onion (41: B8 F8 L8 R9 T8). Worst under words **5.21:1**, bar row 5.16. 17 + 42 + 69 = **128 KB**.
2. **E1-r3-01** chives in soft knife sweeps (41: B8 F8 L8 R9 T8). Worst **5.37:1**, bar row 5.19. 17 + 42 + 70 = **128 KB**.
3. **E1-r3-03** fines herbes: parsley, chives, thyme (41: B8 F8 L8 R9 T8). Worst **5.30:1**, bar row 5.21. **128 KB**.
Base N-r8-01 for comparison: worst 5.30, bar row 5.20, 115 KB.

## How often (proposal; details in OLD_SITE.md)

1 day in 7 the board carries an egg, picked by the local date with the hash `boardVariantIndex` already uses in
`Header.tsx`, so it is the same on every screen and device all day; which egg also comes from the hash. Six days in
seven: the plain N-r8-01. Static art only.

## Still weak

- Self-grades only; no outside panel on other accounts yet. Expect about 1 lower per lens.
- The 5:1 cap means no bit is ever brighter than the lightest wood: white things (onion, garlic, sesame, salt) can
  only be a pale tan. Onion reads by its warm tint and bright edge line, not by real whiteness. Chili and zest are
  muted to near invisible for the same reason.
- Bits are about 1.4x life size so they read at all; at 3x a close look can tell.
- Native weight: every egg shipped adds ~125 KB to the app (5 finals ~640 KB). Web downloads one file per day.
- Seen only in a browser mock; not on a real iPhone/iPad (same caveat as lane N's tile).
- Round 1 and 2 tiles were made with the code as it was in those rounds (the onion and scallion code changed after);
  `make.py r1 --force` today would redraw them with the newer bits.

## Score tables

### Round 1 table

| id | from | what it tries | B | F | L | R | T | sum | worst under words 390 / 820 / 1180 / 1280 / 1280@1x / 1920@1x | phone clock | bar row worst | bits | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E1-r1-01 | - | Chives: rings and a few side pieces, sparse and even | 7 | 7 | 9 | 9 | 7 | 39 | 5.76 / 5.24 / 5.76 / 5.73 / 5.43 / 5.59 | 5.87 | 5.21 | 150 | 16+41+68 = 126 | keep: chive rings read as rings at 3x; even and calm. Phone shows almost none (zone too wide). |
| E1-r1-02 | - | Chives in three soft knife sweeps | 7 | 8 | 8 | 9 | 7 | 39 | 5.74 / 5.37 / 5.81 / 5.34 / 5.42 / 5.42 | 6.02 | 5.23 | 200 | 17+42+67 = 126 | keep: soft knife sweeps look like real prep, not confetti. Best of round 1. |
| E1-r1-03 | - | Diced onion: pale, see-through pieces with a bright layer edge | 5 | 4 | 8 | 9 | 6 | 32 | 5.76 / 5.24 / 5.78 / 5.41 / 5.42 / 5.42 | 5.87 | 5.21 | 120 | 16+41+67 = 124 | fix: onion reads as grey-pink chips (white on orange wood goes grey). Warm it. |
| E1-r1-04 | - | Chives + onion (the classic) | 7 | 6 | 8 | 9 | 7 | 37 | 5.39 / 5.38 / 5.25 / 5.24 / 5.42 / 5.68 | 5.87 | 5.18 | 180 | 17+41+67 = 125 | keep: chives + onion is the brief in one picture; onion needs the fix. |
| E1-r1-05 | - | Flat-leaf parsley flecks | 6 | 6 | 8 | 9 | 7 | 36 | 5.60 / 5.30 / 5.73 / 5.59 / 5.35 / 5.73 | 5.87 | 5.15 | 220 | 17+41+68 = 125 | keep: parsley reads, but even spread looks a little like confetti. |
| E1-r1-06 | - | Cilantro + red onion + lime zest (taco night) | 5 | 5 | 8 | 9 | 6 | 33 | 5.84 / 5.43 / 5.59 / 5.40 / 5.51 / 5.76 | 5.67 | 5.16 | 220 | 17+41+69 = 127 | cut: taco mix looks like a weaker parsley; red onion and lime do not read. |
| E1-r1-07 | - | Thyme leaves + cracked pepper | 6 | 6 | 9 | 9 | 7 | 37 | 5.61 / 5.38 / 5.73 / 5.51 / 5.51 / 5.59 | 5.99 | 5.22 | 330 | 16+40+68 = 125 | keep: peppercorns read well; thyme too small to see. |
| E1-r1-08 | - | Scallion slices + sesame (stir-fry, from the old site) | 4 | 3 | 7 | 9 | 5 | 28 | 5.36 / 5.32 / 5.44 / 5.34 / 5.36 / 5.38 | 5.63 | 5.21 | 200 | 17+41+68 = 126 | fix: scallion reads as round water spots, not slices. |
| E1-r1-09 | - | Fines herbes: parsley, chives, thyme | 7 | 7 | 8 | 9 | 7 | 38 | 5.68 / 5.35 / 5.65 / 5.43 / 5.24 / 5.24 | 5.59 | 5.23 | 270 | 17+42+69 = 127 | keep: parsley + chives + thyme is the most "real cooking" mix. |
| E1-r1-10 | - | Pasta night: parsley, chili flakes, garlic (from the old site) | 6 | 6 | 8 | 9 | 7 | 36 | 5.60 / 5.32 / 5.53 / 5.58 / 5.33 / 5.33 | 5.92 | 5.16 | 240 | 16+40+68 = 125 | keep: pasta night reads; chili flakes are faint (the cap mutes red). |
| E1-r1-11 | - | Rosemary needles + minced garlic + flaky salt | 5 | 5 | 8 | 9 | 6 | 33 | 5.68 / 5.24 / 5.24 / 5.24 / 5.24 / 5.24 | 5.87 | 5.20 | 180 | 16+41+68 = 125 | cut: rosemary needles fine, garlic and salt read as grey. |
| E1-r1-12 | - | Dill + chives + lemon zest | 5 | 5 | 8 | 9 | 6 | 33 | 5.66 / 5.28 / 5.63 / 5.51 / 5.59 / 5.81 | 5.41 | 5.16 | 170 | 16+41+68 = 126 | cut: dill reads as squiggles; chives carry it. |
| E1-r1-13 | - | Cracked pepper + flaky salt (darkest, calmest) | 6 | 7 | 9 | 9 | 7 | 38 | 5.61 / 5.34 / 5.63 / 5.51 / 5.35 / 5.51 | 5.78 | 5.21 | 210 | 16+41+68 = 125 | merge: peppercorns are good; salt grey. Pepper joins thyme in round 2. |
| E1-r1-14 | - | Knife marks only (the old site's "used board", 15 in 100 visits) | 3 | 2 | 10 | 9 | 6 | 30 | 5.55 / 5.24 / 5.24 / 5.24 / 5.48 / 5.48 | 5.93 | 5.22 | 260 | 16+39+67 = 122 | cut: knife marks are invisible at every size (old site kept them, 15 in 100). |

### Round 2 table

| id | from | what it tries | B | F | L | R | T | sum | worst under words 390 / 820 / 1180 / 1280 / 1280@1x / 1920@1x | phone clock | bar row worst | bits | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E1-r2-01 | E1-r1-02 | Chives in soft knife sweeps, one beside the phone clock | 8 | 8 | 8 | 9 | 8 | 41 | 5.37 / 5.42 / 5.65 / 5.30 / 5.43 / 5.72 | 5.51 | 5.20 | 210 | 17+41+69 = 127 | keep: chive sweeps; now one sits beside the phone clock. Main candidate. |
| E1-r2-02 | E1-r1-01 | Chives, sparse and even, a little more of them | 7 | 8 | 9 | 9 | 8 | 41 | 5.42 / 5.22 / 5.79 / 5.42 / 5.45 / 5.51 | 5.99 | 5.21 | 190 | 17+42+69 = 127 | keep: sparse even chives, the quietest. |
| E1-r2-03 | E1-r1-04 | Chives + diced onion (warmer, crisper onion) | 8 | 7 | 8 | 9 | 8 | 40 | 5.66 / 5.27 / 5.30 / 5.34 / 5.40 / 5.26 | 5.87 | 5.20 | 195 | 17+42+69 = 128 | keep: chives + onion; the onion now reads warm and see-through. |
| E1-r2-04 | E1-r1-09 | Fines herbes: parsley, chives, thyme | 8 | 8 | 8 | 9 | 8 | 41 | 5.27 / 5.26 / 5.68 / 5.60 / 5.43 / 5.68 | 5.39 | 5.20 | 290 | 17+42+68 = 126 | keep: fines herbes, a believable mix at 3x and light at 1x. |
| E1-r2-05 | E1-r1-03 | Diced onion alone (warmer, crisper) | 7 | 6 | 8 | 9 | 7 | 37 | 5.47 / 5.32 / 5.30 / 5.47 / 5.31 / 5.59 | 5.48 | 5.15 | 140 | 16+41+68 = 125 | keep: onion alone reads, but could be garlic; add a few chives. |
| E1-r2-06 | E1-r1-07 x E1-r1-13 | Thyme leaves + cracked and whole peppercorns | 7 | 7 | 9 | 9 | 8 | 40 | 5.79 / 5.48 / 5.73 / 5.39 / 5.43 / 5.76 | 5.40 | 5.17 | 330 | 16+41+68 = 126 | keep: thyme + peppercorns, calm; pepper is the darkest, safest bit. |
| E1-r2-07 | E1-r1-05 | Flat-leaf parsley in sweeps, more olive | 7 | 6 | 8 | 9 | 7 | 37 | 5.55 / 5.46 / 5.57 / 5.48 / 5.24 / 5.28 | 5.42 | 5.21 | 230 | 17+42+68 = 126 | merge: parsley sweeps still a bit confetti; becomes gremolata. |
| E1-r2-08 | E1-r1-08 | Scallion rings (crisp) + sesame + a few chili flakes | 5 | 4 | 8 | 9 | 6 | 32 | 5.59 / 5.30 / 5.46 / 5.59 / 5.35 / 5.40 | 5.98 | 5.21 | 198 | 17+41+67 = 125 | fix again: scallion still grey discs; rebuild it like the chive ring. |
| E1-r2-09 | E1-r1-10 | Pasta night: parsley, chili flakes, minced garlic | 6 | 6 | 9 | 9 | 7 | 37 | 5.77 / 5.45 / 5.45 / 5.45 / 5.35 / 5.35 | 5.70 | 5.20 | 245 | 17+41+68 = 126 | cut: pasta night too sparse; chili still faint. |
| E1-r2-10 | E1-r2-01 | r2-01 a step stronger and fuller (tests how far "light" can go) | 7 | 8 | 7 | 9 | 7 | 38 | 5.68 / 5.39 / 5.57 / 5.57 / 5.35 / 5.35 | 5.31 | 5.20 | 260 | 18+42+69 = 129 | test: strength 2.3 still light at 1x but busier at 3x; finals use 2.0. |

### Round 3 table

| id | from | what it tries | B | F | L | R | T | sum | worst under words 390 / 820 / 1180 / 1280 / 1280@1x / 1920@1x | phone clock | bar row worst | bits | KB 1x+2x+3x = all | verdict |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| E1-r3-01 | E1-r2-01 | Chives in soft knife sweeps | 8 | 8 | 8 | 9 | 8 | 41 | 5.83 / 5.37 / 5.90 / 5.41 / 5.43 / 5.51 | 5.88 | 5.19 | 230 | 17+42+70 = 128 | top: chives in soft knife sweeps. The cleanest, most "someone was cooking" egg. |
| E1-r3-02 | E1-r2-03 | Chives + diced onion | 8 | 8 | 8 | 9 | 8 | 41 | 5.76 / 5.21 / 5.26 / 5.24 / 5.40 / 5.42 | 5.36 | 5.16 | 205 | 17+42+69 = 128 | top: chives + diced onion, Tyler's own words; onion warm and see-through. |
| E1-r3-03 | E1-r2-04 | Fines herbes: parsley, chives, thyme | 8 | 8 | 8 | 9 | 8 | 41 | 5.55 / 5.30 / 5.76 / 5.36 / 5.43 / 5.34 | 5.50 | 5.21 | 295 | 17+42+69 = 128 | top: fines herbes (parsley, chives, thyme); the richest mix that stays light. |
| E1-r3-04 | E1-r2-06 | Thyme leaves + cracked and whole peppercorns | 7 | 8 | 9 | 9 | 8 | 41 | 5.59 / 5.33 / 5.61 / 5.43 / 5.43 / 5.26 | 5.46 | 5.22 | 340 | 17+42+68 = 127 | final: thyme + peppercorns; the calmest, darkest bits. |
| E1-r3-05 | E1-r2-02 | Chives, sparse and even (the quietest) | 7 | 8 | 9 | 9 | 8 | 41 | 5.30 / 5.36 / 5.30 / 5.23 / 5.35 / 5.70 | 5.55 | 5.21 | 190 | 17+42+69 = 128 | final: sparse even chives; the quietest egg. |
| E1-r3-06 | E1-r2-05 | Diced onion with a few chives | 7 | 7 | 8 | 9 | 7 | 38 | 5.43 / 5.34 / 5.72 / 5.73 / 5.38 / 5.60 | 5.33 | 5.19 | 160 | 16+40+67 = 124 | final: diced onion with a few chives; onion alone could pass for garlic. |
| E1-r3-07 | E1-r2-07 x E1-r2-09 | Gremolata: parsley, minced garlic, a little lemon zest | 7 | 7 | 8 | 9 | 7 | 38 | 5.59 / 5.47 / 5.48 / 5.43 / 5.43 / 5.59 | 5.48 | 5.21 | 247 | 17+41+69 = 127 | final: gremolata (parsley, garlic, zest); zest barely shows. |
| E1-r3-08 | E1-r2-08 | Scallion rings (rebuilt like the chive) + sesame | 7 | 7 | 8 | 9 | 7 | 38 | 5.59 / 5.24 / 5.58 / 5.43 / 5.48 / 5.48 | 5.79 | 5.21 | 165 | 17+41+67 = 125 | final: scallion rings now read as slices; the white ones run a little cool. |

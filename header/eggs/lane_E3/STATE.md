# Lane E3 state (I-007 part E, Easter eggs) — short; ITERATIONS.md is the archive

## Agreed (Tyler, 11-27)
- Base bar FROZEN = lane N, N-r8-01 board, Fraunces SemiBold Italic 24 name, SC app-icon tile, gold #E2B86A cloud.
- Eggs: now and then the same board shows a very light, diffuse scatter of chopped herbs / chives / onion.
- Every pixel >= 5.15:1 vs cream (after encoding, every width 320-2560); gold cloud >= 3:1; each egg < 130 KB.
- Panel (round 6): medium only; cut thyme + pepper; 1 day in 5, eggs take turns.

## Current finals (round 8, medium, turn order) — self /50
1. E3-r8-01 chives 40  2. E3-r8-04 parsley 38  3. E3-r8-02 chives + white onion 36
4. E3-r8-03 red onion 39  5. E3-r8-05 scallion 36 (first to cut)
- Worst cream 5.16:1, gold 3.04:1+, food behind words 0.0% at all 11 shot widths, 115-117 KB each;
  580 KB for 5 (465 KB for 4). Faint/medium pair kept in the gallery: E3-r7-01f / E3-r7-01m.
- Schedule: N = 5, 5 eggs, 73 egg days/yr, gaps 2-8, 0 back-to-back in 10 years; pins in SCHEDULE.md.

## How (gen/egg7.py, recipes gen/eggs_r7.py, gen/eggs_r8.py)
- Keep-out map of every word + island/notch at every width; hero, mid group, sprinkle, strip and (r8) field
  bits tested by their real drawn shape. The phone hero lives in the row's word-free top / bottom strips.
- shoot.py: 393 island app, 390 notch app, 390/375/360/320 web, 820, 1180, 1280 (2x, 1x), 1920 1x;
  "behind words" = % of word-box px changed > 30 levels vs base (WebP noise alone reaches ~27).

## Open (not fixed; say so to Tyler)
- White onion still tan, not white (the 5.15 cap forbids anything lighter than the lightest wood).
- Calmer than the old website's eggs. Scallion may read as O-rings. 1x desktop = "look for it".
- Not seen on a real iPhone/iPad; no outside panel on rounds 7-8.

CHECKPOINT r7 done (6 tiles) | next: r8 final set.
CHECKPOINT r8 done (5 finals; gallery, desktop, ITERATIONS, SCHEDULE rebuilt) | next: outside panel on r8 and
Tyler's pick (5 or 4 eggs), then the build in Header.tsx + native assets.

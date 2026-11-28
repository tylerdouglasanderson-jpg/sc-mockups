# How the old website did its "changes every now and then" board

## What I found

- **The code:** `C:/MealPlanner/design/claude_design/project/ui_kits/website/header-rotation.js` (the marketing-site kit
  from the Claude Design bundle, May 2026; still says "Mise"). Its source of truth is
  `design/claude_design/project/explorations/header-rotation.jsx` (+ `header-rotation.html`, a demo page), which drew
  ~25 ingredients and 6 mixes.
- **What it drew:** an SVG laid OVER the board (`.site-header`, `.section--butcher`, `.frame__chrome`) at run time,
  tiny shapes at 0.85-0.95 opacity: parsley (green ellipses), chili flakes, scallion rings (cream disc + green ring),
  chives (thin green bars), sesame, citrus zest, garlic skin, and "knife marks" (thin black lines). Mixes: "Pasta night"
  (parsley + chili + garlic skin) and "Stir-fry" (scallion + sesame + chili + garlic). Flour was tried and removed
  ("it didn't read right on the wood").
- **How often:** a weighted pick, **70 in 100 plain board, 15 knife marks, 15 food** (parsley 4, chili 3, scallion 2,
  chives 2, sesame 1, zest 1, pasta night 1, stir-fry 1).
- **How it picked:** **random per browser session**, not by date. A seed is stored in `sessionStorage`
  (`mise-butcher-seed`), so the pick holds while you click around and changes in a new session; two people (or two
  devices) see different boards the same day. Density scales with the surface's area (per 820x44 px).
- **The app today:** `C:/mise-rebuild/app/src/components/Header.tsx` already has the hook: `BOARD_VARIANTS` (one row),
  `boardVariantIndex(dateKey, count)` (FNV-1a hash of the LOCAL date, "the same day always draws the same board, on
  every screen and every device"), `useBoardVariant()`. Its comment cites walk decision D7 A (2026-10-08): "it should
  vary a little day to day (e.g. a random chance of chopped onions in the background)". No egg art was ever made for it.
- Searched and found nothing else: `git log -S chive|onion|chopped` in C:/MealPlanner (only docs and recipe text),
  the app's `assets/brand` (only `endgrain-bp.svg`).

## What lane E1 keeps and changes

| Old site | Lane E1 |
|---|---|
| ~30 in 100 visits not plain (15 food, 15 knife) | **1 day in 7 an egg** (~14%, close to the old 15% food share). Knife marks cut: drawn at the same weight they cannot be seen on this board. |
| Random per session (sessionStorage) | **By the local date**, the app's `boardVariantIndex` hash: same egg on every screen and device all day. |
| Live SVG overlay, 0.85-0.95 opacity, bright greens/reds | **Baked into the tile** (one picture, no overlay, no layout code), low opacity, muted sage/olive greens, warm onion. Every pixel still gives cream text 5:1 or better. |
| Uniform scatter everywhere, behind the words too | Diffuse field + a few soft knife "sweeps"; the mark + name stay clear; a light dip at the account spot. |
| Parsley, chili, scallion, chives, sesame, zest; pasta night, stir-fry | Same family: chives, onion, parsley, thyme, pepper, scallion + sesame, gremolata; pasta night tried (round 1-2) and cut (chili too faint under the contrast cap). |
| Static | Static. |

## The proposal (how often)

```ts
// Header.tsx: one board every day; on 1 day in 7 the same board with an egg baked in.
const EGGS = [/* E1-r3-02, -01, -03, -04, -05 ... as BoardVariant rows */];
export function boardForDay(dateKey: string): BoardVariant {
  const h = fnv1a(dateKey);               // the hash boardVariantIndex already uses
  if (EGGS.length === 0 || h % 7 !== 0) return BOARD;   // 6 days in 7: the plain N-r8-01
  return EGGS[Math.floor(h / 7) % EGGS.length];         // which egg: the same hash, no fixed order
}
```

- 1 in 7 over the long run, but not every 7th day (the hash scatters it). Same on web, iPhone, iPad.
- Web downloads only the one file it shows (`image-set`), so an egg day costs 17-70 KB once.
- Native bundles every egg it may show: about 125 KB each (1x + 2x + 3x). Shipping 5 finals = ~640 KB in the app.
  Cheaper: ship 3 (the top 3, ~385 KB), or ship only @2x/@3x on iOS.

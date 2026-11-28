# I-007 part E: when an egg shows (take turns, not a pure hash)

2026-11-27, lane E3, re-run for the FINAL count (round 8: 5 eggs). Panel finding: a pure date hash left some eggs
unseen for months and allowed back-to-back egg days. This one takes turns. All three panel lenses agreed with
1 day in 5 and with taking turns.

## Rule

- Count local calendar days. Cut them into blocks of N days.
- In each block exactly ONE day is an egg day. A hash of the block number picks which day, but never the block's
  last day, so two egg days are never back to back.
- Which egg = block number mod egg count, so the eggs take turns in a fixed order; every egg shows once per
  N x count days (25 days with 5 eggs, 20 with 4).
- Same answer on every screen and device (pure function of the local date), changes at the person's own midnight,
  no start date to store, never animated.

## Pick: N = 5

Tyler asked for something seen "every now and then", and the eggs are light; 1 in 7 means a person who opens the app
on some days only may see one or two a month. N = 5 still leaves 4 plain days in 5.

## Turn order (5 eggs)

`BOARD_VARIANTS` = [N-r8-01 (plain), E3-r8-01 chives, E3-r8-04 parsley, E3-r8-02 chives + onion, E3-r8-03 red onion,
E3-r8-05 scallion]. The two chive eggs are never on back-to-back egg days, including across the wrap. If Tyler cuts
scallion, drop the last entry: the same order still keeps the chive eggs apart (red onion wraps to chives).

## Simulation (2027; `gen/schedule.py`, output `schedule.json`)

| N | eggs | egg days / year | longest gap | shortest gap | back-to-back | times each egg shows |
|---|---|---|---|---|---|---|
| **5** | **5** | **73** | **8 days** | 2 days | 0 | 14-15 |
| 5 | 4 | 73 | 8 days | 2 days | 0 | 18-19 |
| 7 | 5 | 53 | 12 days | 2 days | 0 | 10-11 |

Ten years from 2026-01-01 (N = 5): 0 back-to-back egg days.
Next egg days with N = 5 and 5 eggs: Mon 11-30 chives + onion, Sun 12-06 red onion, Tue 12-08 scallion,
Sun 12-13 chives, Mon 12-21 parsley, Fri 12-25 chives + onion, Tue 12-29 red onion, Sat 01-02 scallion.

## The function for `src/components/Header.tsx`

Replaces the plain day pick (`boardVariantIndex`) with "base most days, an egg in turn". Same FNV-1a as today.

```ts
/** Easter eggs (I-007 E): the plain board most days; one egg day per block of EGG_EVERY days, the eggs in turn. */
export const EGG_EVERY = 5;

function fnv1a(s: string): number {
  let h = 0x811c9dc5;
  for (let i = 0; i < s.length; i += 1) {
    h ^= s.charCodeAt(i);
    h = Math.imul(h, 0x01000193) >>> 0;
  }
  return h;
}

/** dateKey = the person's local 'YYYY-MM-DD' (localTodayIso). Returns -1 for the plain board, else the egg index. */
export function eggIndexForDay(dateKey: string, eggCount: number, every: number = EGG_EVERY): number {
  if (eggCount < 1 || every < 2) return -1;
  const [y, m, d] = dateKey.split('-').map(Number);
  const day = Math.floor(Date.UTC(y, m - 1, d) / 86400000);   // calendar day number; UTC maths on LOCAL parts
  const block = Math.floor(day / every);
  const pick = fnv1a(`egg-block-${block}`) % (every - 1);       // never the block's last day: no back-to-back
  return day - block * every === pick ? block % eggCount : -1;
}

/** BOARD_VARIANTS[0] = the plain board N-r8-01; the rest are the eggs, in turn order. */
export function boardVariantFor(date: Date, variants: readonly BoardVariant[] = BOARD_VARIANTS): BoardVariant {
  const egg = eggIndexForDay(localTodayIso(date), variants.length - 1);
  return egg < 0 ? variants[0] : variants[1 + egg];
}
```

`useBoardVariant` keeps its shape (memo on the day key) and calls the same logic. Test: the Python in
`gen/schedule.py` is a line-for-line twin. Pins for 5 eggs (egg index into the turn order above):
2026-11-30 -> 2 (chives + onion), 2026-12-01 -> -1 (plain), 2026-12-06 -> 3 (red onion), 2026-12-08 -> 4 (scallion),
2026-12-13 -> 0 (chives), 2026-12-21 -> 1 (parsley); and no two consecutive days are both eggs over 10 years.
With 4 eggs the egg DAYS are the same; only which egg changes (block mod 4) — recompute the pins if scallion is cut.

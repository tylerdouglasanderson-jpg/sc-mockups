# I-007 build notes: one header bar on every page (lane N, round 9)

**Nothing here is built.** Ship web, iPhone and iPad in the SAME piece of work
("all apps change together"; DESIGN 4.1.6). App repo `C:/mise-rebuild/app`.

**Agreed by Tyler, 11-27 17:27:** board **N-r8-01** ("I definitely like the first one the most"), a 56 bar, the SC mark
("that it's the brightest thing on the bar is perfectly fine"), and the bar on the kitchen iPad at rest.
**Still waiting on Tyler: name size, Fraunces 22 vs 24 vs 26 (`name_compare.html`).** He said "yes to both" to
"'SupperCraft' bold at 24 (today semibold 22) and a 56 bar", but the gallery he saw drew the name in IBM Plex Bold
Italic, not the app's face. The face stays Fraunces SemiBold Italic (no Plex, no new font file).

**Checked against `origin/main` 30f213f1b (2026-11-27 16:16).** Every file:line below is at that commit. The main
checkout at `C:/mise-rebuild/app` is an old branch (`ai-key-mode-toggle`, 11-22 14:37); do not read it for this work.
The round-8 panel read that old checkout, so several of its findings describe code that is already gone (see 0.2).

## 0. Every brown bar and every "SupperCraft" name in the app

### 0.1 Bars (all draw `Header.tsx` → `kit/layer/TopInsetBoard.tsx`, except the rail strip)

| # | Code (origin/main) | Row today | What is in it | Pages | Becomes |
|---|---|---|---|---|---|
| 1 | `src/components/PrimaryHeader.tsx:345-356` (row), `:379` (name), `:383-387` (status slot), `:389-419` (avatar), `:305` (web menu top `headerRow - 3`) | 50 (`FRAME.headerRow`) | name 22 as the home link (`ShellAction layout="pr-8"` = 32 pad); status slot: saving sign (built, `kit/SavingSign.tsx`), timer (empty); avatar 29 + cream ring in a 44 target | every signed-in page on a phone and every unframed page: Today, Plan, Groceries (+Put Away), Kitchen, Recipes (+recipe, new recipe, import), Prep, History, Leftovers, Reminders, Settings, About, Capture, Kitchen Setup (`SetupChrome.tsx:49`), admin, tickets | 56 row, `BrandLockup`, web menu top `headerRow - 6` |
| 2 | `app/_layout.tsx:149-153` (`PrimaryHeader frameLead={lead}`) | 50 | the same bar drawn ONCE across rail + page; name at `frameHeaderLead()` (`kit/frame/frameHeader.ts:29`): 8 beside the wide rail, 10 beside the slim rail | iPad and web 700+, every signed-in page | 56; lockup at `railIconX()` = 22 (see 3.6) |
| 3 | `src/kit/frame/Rail.tsx:48` (own `require('endgrain-bp.svg')`), `:56-64` `RailBoard` | inset + 50 | board strip, no words | rail top, iPad and web | inset + 56; uses the one shared texture |
| 4 | `src/components/entry/EntryShell.tsx:96-102` `EntryBar` (+ `:112-143` `EntryHomeLink`) | 50 | name 22 only | 11 entry pages: sign-in, sign-up, forgot-password, reset-password, check-email, confirm, auth/callback, auth/finish-setup, invite/[token], remove-email, +not-found | 56, `BrandLockup` |
| 5 | `src/components/entry/EntryParts.tsx:500-506` `EntryHeader` | 50 | name 22 (plain text until home is ready, M2) + ringed avatar 29, not a button | `app/welcome.tsx:228-242`, `app/onboarding.tsx:427-432` | 56, `BrandLockup` |
| 6 | `src/components/grocery/ShopParts.tsx:165` (`SHOP_SIZE.shopperHeader: 58`), `:234` `ShopHeader`; `app/shop/[token].tsx:44-56` `ShopShell` | **58** | name 22 + "Shared shopping list" (`[token].tsx:50`, meta, cream) | the shopper link (live and ended) | 56, `BrandLockup`, nothing at the right; the words move to the page |
| 7 | `src/components/kitchen/KitchenHeader.tsx:15-24` | **44** (no height passed: `Header`'s default class `h-hdr-landscape`, `tailwind.config.js:87`) | name 22 + "Pick Your Name" + empty guest avatar (`KitchenPickName`) | kitchen iPad awake, nobody signed in (`app/index.tsx:979`) | 56, `BrandLockup` |
| 8 | `app/entry.tsx:136-138` | **44** (same default) | name 22 only | kitchen iPad "Who is this?" | 56, `BrandLockup` |

**Count: 8 bar kinds today, 3 row heights (50, 58, 44), one name everywhere (Fraunces SemiBold Italic 22), no mark on any.**
**Plus one place that GAINS a bar (agreed):** 9, the kitchen iPad at rest (3.7).

Names with no brown bar (no change unless noted):

| Code | What |
|---|---|
| `src/components/cook/CookExtras.tsx:27` `CookBand`, `:110` `CookTopBand` | Cook: tan band 46 that owns the status bar; no brown bar (DESIGN 8.1.2). Agreed: stays so. |
| `src/kit/AmbientRest.tsx` via `kitchen/KitchenRestGate.tsx` | kitchen iPad at rest: today full screen, clock + words, no bar (DESIGN 8.4.5). **Gets the bar** (Tyler agreed, 11-27 17:27). |
| `app/about.tsx:96` + `:107` | About: a PrimaryHeader AND a 28 brand-brown name in the page head = the name twice on one screen, against DESIGN 2.12.3. Not this job; flag it. |
| `src/kit/gate/BoardCard.tsx:72` | loading board card, name 28 |
| `src/kit/gate/WelcomeBack.tsx` | Welcome Back, name 50 / 76 |
| `src/kit/catalog/*` (FoundationPages 254-256, PageStripPage 32, ActionPages 283-286) | kit catalog swatches only |

### 0.2 What the round-8 panel described that is no longer true on origin/main

| Panel said (11-22 checkout) | origin/main |
|---|---|
| Phone / upright iPad sign-in has no bar and a big 28 name + "Your kitchen, in rhythm." | Since 11-23 05:24 (604e292a8, walk C-022) every entry page, sign-in included, has `EntryBar` (50, name 22, nothing else). "Your kitchen, in rhythm." is the page HEADLINE (`sign-in.tsx:211`), not a byline. No 28 name on sign-in. |
| `StoryFrame` (EntryShell 289-296): 28 name + italic note in a 58+ bar | gone (same commit); the story pages use `EntryBar` |
| Welcome / onboarding 58 (`ENTRY_SIZE.storyHeader`) | gone; `EntryHeader` uses `FRAME.headerRow` (50) |
| `SetupChrome.tsx:23` empty 58 board | Kitchen Setup uses `PrimaryHeader` (`SetupChrome.tsx:49`) |
| Name is Plex SemiBold Italic; plan: Plex Bold Italic 24 + a new `IBMPlexSans_700Bold_Italic.ttf` | The name is **Fraunces 144pt SemiBold Italic** (Tyler, walk C-019, 11-22 19:06; `kit/wordmarkFont.ts`). Round 8's Plex 700 plan is **withdrawn**: it would undo Tyler's pick. |
| Still true | shop 58 + "Shared shopping list"; `headerRow` 50; `scales.js:61` `wordmark = { header: 22, signIn: 28 }`; `Rail.tsx:48` own texture; `TopInsetBoard` 720x108 / cover; web menu `headerRow - 3` (`PrimaryHeader.tsx:305`); avatar one 1.5 cream ring |

## 1. The design in one line

Every bar is ONE component: the board, a **56 row**, on the left **`BrandLockup`** (the app icon tile 26, an 8 gap,
the app's `Wordmark`; size waiting on Tyler, section 8), on the right only what that page needs (account, status slot, or nothing), a 1 px
`header-rule` line at the bottom. Same height, same background, same logo on every page (Tyler, 11-27 15:28).

- Mark: the **real icon file** `assets/brand/favicon-tile.svg`, untouched (DESIGN 2.12.6: "Do not redraw it").
  Round 8's tile with "sc" 14% larger is withdrawn. Lane N's `favicon-tile.svg` is byte-identical to the app's.
- Name: `Wordmark size="header"`, face stays **Fraunces SemiBold Italic**. Size: **waiting on Tyler: Fraunces 22 vs 24
  vs 26 (`name_compare.html`)** (today 22, line 28). Same weight and file at every size, so the 28 names on About, the
  loading board card and Welcome Back are untouched, and **no font file changes**.
- Board: **N-r8-01**, the agreed board (Tyler, 11-27 17:27: "I definitely like the first one the most"; passed the
  final panel at 8). N-r9-01 (same recipe, no near-closed ring targets; not panel-graded) is only an option he did not
  pick.

## 2. Assets

| File (new, app repo) | From lane N | Size | Used by |
|---|---|---|---|
| `assets/brand/board.webp` | `tiles/N-r8-01@1x.webp` (1440x140) | 15 KB | native 1x |
| `assets/brand/board@2x.webp` | `tiles/N-r8-01@2x.webp` (2880x280) | 36-37 KB | native 2x (iPad) |
| `assets/brand/board@3x.webp` | `tiles/N-r8-01@3x.webp` (4320x420) | 59-61 KB | native 3x (iPhone) |
| `assets/brand/web/board-1x.webp`, `-2x`, `-3x` | the same three files | 109-113 KB | web `image-set` (no `@` in the name, so Metro does not fold them into one scaled asset) |

- The mark needs no new file: `require('../../assets/brand/favicon-tile.svg')` as the app already ships it (as an
  image on native via expo-image, the same way the board SVG is drawn today).
- **Blocks are 36 wide x 28 tall** (5 rows of 28 in the 140 tile; 40 columns of ~36 in 1440). Never write "36 px
  blocks" or "36 pt square".
- Keep `endgrain-bp.svg` until web, iPhone and iPad are all switched, then delete it (300 KB).
- **Never re-encode the WebP files** in a build step. Each was checked pixel by pixel after encoding (lossy WebP lifts
  single pixels next to dark detail by up to ~30%; `gen/board_n.py` `encode_safe` darkens just those spots). Every
  pixel of every shipped file gives cream `#FAF4EB` **5.15:1 or better** (N-r8-01 5.17, N-r9-01 5.16). Anything that
  re-encodes them (a CDN, an asset optimiser) must re-run that check.
- **PNG fallback** (only if native `resizeMode="repeat"` misbehaves with WebP on a device): make `board@Nx.png` from
  the same source with `board_n.finish()` and run the **same pixel-by-pixel check on the PNG files** (PNG is lossless,
  so it should pass as the source does, but measure it: 5.15:1 at every pixel). PNG is ~3-4x heavier.

## 3. Code, file by file

### 3.1 `src/kit/frame/metrics.ts:36`
`headerRow: 50` → `56` (comment: "two whole 28-tall rows of the 1440x140 board tile"). Every bar and the rail strip
read it. Knock-ons that follow automatically: `kit/PageShape.tsx:294`, `CaptureParts.tsx:358`
(`CAPTURE_STICKY_CHROME`), `kit/CapturePopover.tsx:57`, `Rail.tsx:340`.

### 3.2 One texture source + one lockup
- New `src/kit/layer/boardTexture.native.ts` / `.web.ts`:
  ```ts
  // native
  export const HEADER_BOARD = require('../../../assets/brand/board.webp'); // Metro adds @2x/@3x
  // web
  export const HEADER_BOARD = { x1: require('../../../assets/brand/web/board-1x.webp'),
    x2: require('../../../assets/brand/web/board-2x.webp'), x3: require('../../../assets/brand/web/board-3x.webp') };
  export const BOARD_TILE = { width: 1440, height: 140 } as const;
  ```
- `src/components/Header.tsx:27-29`: `BOARD_VARIANTS = [{ id: 'n-r8-01', texture: HEADER_BOARD }]`.
- `src/kit/frame/Rail.tsx:48`: drop its own `require`; use `useBoardVariant().texture` so the rail strip and the bar
  can never show two boards.
- **`Header.tsx:69`: the row's height becomes `FRAME.headerRow` inside `Header` itself** (replace the default
  `className="h-hdr-landscape"`, 44). Then delete every caller's own height: `PrimaryHeader.tsx:349-351` (keep web's
  `overflow:'visible', zIndex:100`), `EntryShell.tsx:98`, `EntryParts.tsx:502`, `ShopParts.tsx:234` and
  `SHOP_SIZE.shopperHeader` (`:165`). `KitchenHeader.tsx:15` and `app/entry.tsx:136` then get 56 with no edit. One
  place owns the height: a page cannot drift again.
- New `src/kit/BrandLockup.tsx`: the icon tile (26, `accessible={false}`, decorative: the link already says
  "SupperCraft home"), an 8 gap, `<Wordmark size="header" onDark testID={wordmarkTestID} />`. If Tyler picks 24 or 26,
  change `wordmark.header` in `scales.js:61` (line height to match), not the component. Used INSIDE the existing
  link/plain wrappers, so the home-link rules stay as they are:
  `PrimaryHeader.tsx:379`, `EntryShell.tsx:126` and `:140` (`EntryHomeLink`, which `EntryBar`, welcome and onboarding
  already share), `[token].tsx:49`, `KitchenHeader.tsx:18`, `app/entry.tsx:137`.

### 3.3 `src/kit/layer/TopInsetBoard.tsx`
Web, `webTileStyle` (`:19-24`):
```ts
const uri = (a: unknown) => (typeof a === 'string' ? a : (a as { uri?: string } | null)?.uri ?? null);
export function webTileStyle(t: Texture): ViewStyle | null {
  const s = t as unknown as { x1?: unknown; x2?: unknown; x3?: unknown };
  const u1 = uri(s.x1), u2 = uri(s.x2), u3 = uri(s.x3);
  if (!u1 || !u2 || !u3) return null;                      // flat bg-header shows: honest degradation
  return { backgroundImage: `image-set(url("${u1}") 1x, url("${u2}") 2x, url("${u3}") 3x)`,
    backgroundSize: '1440px 140px', backgroundPosition: 'left bottom', backgroundRepeat: 'repeat' } as unknown as ViewStyle;
}
```
`image-set()` unprefixed: Chrome 113+, Safari 17+, Firefox 88+; older browsers get the flat brown. A browser
downloads ONE file (15 / 37 / 61 KB).

Native (`:46`, replaces `<ExpoImage contentFit="cover">`):
```tsx
<Image source={texture} resizeMode="repeat"
  style={{ position: 'absolute', left: 0, right: 0, bottom: 0, height: BOARD_TILE.height }} />
```
The tile repeats from the Image's top-left; with `bottom: 0, height: 140` its rows line up with the bar's bottom
like web. Keep `NATIVE_CLIP`. Tallest board: iPhone 59 inset + 56 = 115 < 140. The 1 px rule: a child View at the
bottom, `height: 1`, class `bg-header-rule`.

### 3.4 `src/components/PrimaryHeader.tsx`
- `:305` web menu top `FRAME.headerRow - 3` → **`FRAME.headerRow - 6`**: the 44 avatar is centred in the row, so at
  56 it ends at 50 and the menu must start at 50 (pointer path, per the comment at `:303-304`). Fix the comment.
- `:379` → `<BrandLockup …>`.
- Row right padding 16 → **8 on phones only**, so the avatar circle's edge sits 15.5 from the edge like the mark's 16.
  Beside a rail keep 16 (3.6).
- Bar text does not grow with system text size: `maxFontSizeMultiplier={1}` on the Wordmark in bars, "Saved", the
  timer count (the menu and screen readers carry the full words).

### 3.5 Status slot (DESIGN 4.6.4, 4.6.5; `HEADER_STATUS_SLOTS` `:75`)
- Saving: `SavingSign` is already built. Unchanged, except its colour (question 5): the gold cloud is Icon tone
  `gold` = `amber` #C8943A, which measures **2.2-2.9:1** against the lightest wood under it (today's bar 2.21; the new
  board 2.36-2.94). An icon that carries meaning needs 3:1. `#E2B86A` gives 3.2-4.3:1 on the new board (3.22 today).
- Timer (`statusSlotContent`, `:81-85`, still empty): ONE timer icon **with a count** (how many timers are open), not
  a countdown, in a 44 target; colour for its state, a shake when one rings, a tap opens all timers. Cook's
  `CookBarButton` (`CookExtras.tsx`) is the model.
- Narrow phones (measured at name size 22 only; at 24 the name is 117 px, at 26 it is 127 px, so **re-measure if Tyler
  picks either**), measured with the real Fraunces name (107 px) + mark, worst case "Saved" + timer + account:
  360, 375, 390 fit as they are (23-105 px to spare); the count always shows. At **320** one rule fires: the name
  link's invisible trailing tap pad (`pr-8`, 32) shrinks as low as 15; nothing visible moves. Back-up steps never
  needed at 320+: "Saved" pads 8 → 4, then the timer's 44 target may overlap its neighbour by 6.
- Screen readers always hear "Saving" / "Saved" and the timer count.

### 3.6 Wide screens: `src/kit/frame/frameHeader.ts:29-34`
`frameHeaderLead()` returns 8 (wide rail) / 10 (slim rail). Since C-074 the rail icons sit at **22 on both rails**
(`Rail.tsx:141` `railIconX()`: gutter 8 + row pad 14). With the mark at 8 the tile looks jammed in the corner while
the avatar circle sits 23.5 from the right (panel L8). Pick: **the lockup starts at `railIconX(slim, insetLeft)` =
22**, in line with the rail icons under it; keep row right padding 16 beside a rail, so the avatar circle edge is
23.5 from the right (even within 1.5). Shown at 1280 and 1180 against 8 and 16-both-sides in `desktop.html`.

### 3.7 Pages
- **Sign-in and the 10 other entry pages:** only the bar changes (56, lockup, board). Nothing top right. No "Sign
  in" button in the bar on sign-up: DESIGN 4.1.7 says the entry bar holds the name and nothing else, and the card's
  footer already says "Already have an account? Sign In".
- **Shopper link:** delete `[token].tsx:50` ("Shared shopping list" in the bar) and the `justify-between` wrapper;
  add the same words as the page's eyebrow (`ShopText kind="label" caps tone="muted"`) above "N of M picked up".
- **Welcome / owner setup:** lockup; keep the ringed avatar at the right; the name stays plain text until home is ready.
- **Kitchen iPad awake** (`KitchenHeader`) and "Who is this?" (`app/entry.tsx`): lockup; 56 via `Header`.
- **Kitchen iPad at rest** (`src/kit/AmbientRest.tsx` via `kitchen/KitchenRestGate.tsx`): **add the bar** (Tyler agreed,
  11-27 17:27: "For number seven, I agree."). The same 56 `Header` + `BrandLockup` as the awake iPad; the mock
  (`gen/pages_r9.py` `kitchen_ipad('new')`) puts the lockup at 22 and "Pick Your Name" at the right.
- **Cook:** no brown bar (agreed).
- Avatar: no change (`Avatar.tsx` `ring` already draws one 1.5 cream border).

## 4. Tests that will break (origin/main)

| Test | Line | Why |
|---|---|---|
| `src/components/__tests__/PrimaryHeader.test.tsx` | 158, 725 | expect height 50 |
| same | 161 | wordmark fontSize 22: still passes if the lockup keeps `testID="primary-wordmark"` on the Wordmark |
| same | 952-961 | menu top `headerRow - 3` → `- 6` |
| `src/components/entry/__tests__/EntryShell.test.tsx` | 100, 102 | `FRAME.headerRow` toBe 50; entry-header height 50 |
| `src/components/entry/__tests__/EntryShell.ipad.test.tsx` | 121 | entry-header height 50 |
| `app/__tests__/welcome.test.tsx` | 682 | welcome-header height 50 |
| `src/components/__tests__/HeaderBoardVariant.test.tsx` | 13, 15, 58 | variant id `endgrain` |
| `src/kit/layer/__tests__/layer.headerTopInset.test.tsx` | 20 | `backgroundSize: '720px 108px'` → `'1440px 140px'`, `backgroundPosition: 'left bottom'`, `backgroundImage` starts `image-set(`; add a case where one of x1/x2/x3 has no URI → `null` |
| `src/kit/layer/__tests__/layer.topInsetBoardWeb.test.tsx` | 17, 25 | pass `texture="/t.svg"` (a string): the new `webTileStyle` returns null for it; give them an x1/x2/x3 object |
| uses `FRAME.headerRow` symbolically, follow on their own | — | `history-detail.test.tsx:171`, `inventory.ledger.test.tsx:59`, `admin.test.tsx:136`, `AppFrame.test.tsx:415, 425, 695` |
| `ShopParts` / shop page tests | — | none pin 58 or "Shared shopping list" today; add one that the bar has no label and the eyebrow shows |
| Unchanged at size 22 (round 8 said they would break; they do not now) | — | `actions.holdsWordmarkCapture.test.tsx:106-113`, `fonts.test.ts`, `foundations.test.ts:444-479`: no font or weight change. At 24 or 26, re-check these and `PrimaryHeader.test.tsx:161` for the size |
| Kitchen rest tests | not checked | the at-rest screen gains a bar; run the `AmbientRest` / `KitchenRestGate` tests |

New tests: `BrandLockup` renders the icon tile (decorative) + Wordmark; every bar kind (1-9) renders `BrandLockup`
and is 56; native `TopInsetBoard` renders an `Image` with `resizeMode="repeat"`, `bottom: 0`, `height: 140`; the
rail strip's texture is the same object as Header's.

## 5. `app.json`, fonts, builds

- **No font change, so `app.json` is untouched.** (Round 8 planned a new `IBMPlexSans_700Bold_Italic.ttf` in BOTH
  font lists: the iOS `expo-font` path list, `:73-81`, and the Android family definitions, `:84-178`. That plan is
  withdrawn with the Plex name. If the name's face ever changes again, it goes in both lists and needs a new app
  build, DESIGN 2.12.1.)
- No new native module: the change is JS + image assets, which `expo-updates` (in `package.json`) can deliver. A new
  native build is not required for this; a TestFlight build is still the simplest way to run the device gate below.

## 6. Ship gates

1. **Device check, iPhone (3x) and iPad (2x), before the board is called standard**: native `resizeMode="repeat"`
   with the @2x/@3x WebP has only been drawn in a browser. Look for: blocks 36 wide x 28 tall, whole rows at the
   bar's bottom, no seam every 1440, no blur, the 1 px rule. If it fails, ship the PNG fallback (2) with its own
   pixel check.
2. Never ship the new tile with native still on `cover` (blocks scale, rows cut; shown in the gallery).
3. Re-run the pixel contrast check on any re-encoded or PNG tile: 5.15:1 at every pixel.
4. Every bar kind 1-9 measured at 56 with the lockup (test above) and seen once on web 390, 1280 and iPad.

## 7. DESIGN.md (change in the same work)

- 4.1.1: "…a texture that varies by day" → "…one board everywhere: a 1440x140 tile of end-grain blocks 36 wide x 28
  tall, drawn at that fixed size and anchored to the bar's bottom on iPhone, iPad and web." (Drop "varies by day":
  Tyler agreed one board.)
- 4.1.4: "member colour with a bolder outline and a thin cream ring" → "member colour with one thin cream ring" (what
  the code already does).
- 4.1.7 (entry pages): "the same height as the signed-in top bar" stays true; add "and the same lockup".
- New 4.1.9: "Every brown bar is the one `Header`: a 56 row (two whole board rows) plus the status-bar inset, on every
  page and size. Left: `BrandLockup` (the app icon tile 26, then the name at the size Tyler picks), at 16 on a phone and in line with the
  rail icons (22) beside a rail. Right: only what the page needs: the status slot then the account; the ringed avatar
  on welcome and setup; 'Pick Your Name' on the kitchen iPad; nothing on entry pages and the shopper link. Words in the
  right corner are always tappable. It ends in a 1 px `header-rule` line, never a shadow. The kitchen iPad at rest has
  it too. Exception: Cook (8.1.2) has no brown bar."
- 8.4.5 (kitchen iPad at rest): change it to say the rest screen shows the bar.
- New 4.1.10: the narrow-phone rule (3.5).
- 2.12.3 / 2.12.6: add "the bar shows the icon tile before the name (the icon file itself, never redrawn)".
- Tokens (`palettes/light.js`): add `'header-rule': 'rgba(20,8,0,0.55)'`; if question 5 is yes, a bar-only gold for
  the saving cloud (e.g. `#E2B86A`). `header` #6B3E14 stays the flat fallback (the board's 56-row average is #6E4019
  / #6F4019).

## 8. Tyler's answers and open questions

Agreed (11-27 17:27):
- Board: **N-r8-01**. N-r9-01 is only an option.
- Mark: the icon tile before the name.
- Bar: 56.
- Kitchen iPad at rest: **add the bar.**
- Nothing else on the bar. Cook keeps its tan band, no brown bar.
- One board every day. He also asked for now-and-then "Easter egg" scatters (chopped chives, onions, herbs): a second
  build, after the base bar and once agreed (`../BRIEF.md`, part E).

Open:
- Name size: **waiting on Tyler: Fraunces 22 vs 24 vs 26 (`name_compare.html`)**. The face stays Fraunces (no Plex, no
  new font).
- Question 5, lighter gold for the saving cloud on the bar (#E2B86A, 3.2:1+ vs 2.2:1 today)? **Pick: yes.** No answer
  to this one is recorded in `../BRIEF.md`; check before building it.

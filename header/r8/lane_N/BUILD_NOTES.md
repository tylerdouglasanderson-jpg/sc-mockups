# I-007 build notes: the header bar (lane N pick)

**Nothing here is built. Every change waits on Tyler's OK.** Ship web and native in the SAME piece of work
(DESIGN 4.1.6, "all apps change together"); the tile must never ship with native still on `cover`.

Pick: board **N-r8-01**, the bar in `gen/mock.py`. App repo: `C:/mise-rebuild/app`.

## 1. Assets

| File (new) | From lane N | Size | Used by |
|---|---|---|---|
| `assets/brand/board.webp` | `tiles/N-r8-01@1x.webp` (1440x140) | 15 KB | native 1x (and Android mdpi) |
| `assets/brand/board@2x.webp` | `tiles/N-r8-01@2x.webp` (2880x280) | 37 KB | native 2x |
| `assets/brand/board@3x.webp` | `tiles/N-r8-01@3x.webp` (4320x420) | 61 KB | native 3x |
| `assets/brand/web/board-1x.webp`, `-2x`, `-3x` | the same three files | 113 KB | web `image-set` (no `@` in the name, so Metro does not fold them into one scaled asset) |
| `assets/brand/sc-mark.svg` | `favicon-tile-n114.svg` | 4 KB | the bar's mark (true icon tile #FAF4EB, "SC" 14% larger) |

- Keep `endgrain-bp.svg` until both apps are switched, then delete it (300 KB).
- Never re-encode the WebP files in a build step: each was checked pixel by pixel after encoding (lossy WebP lifts
  single pixels next to dark detail by up to ~30%; `gen/board_n.py` `encode_safe` darkens just those spots).
  If anything re-encodes them, re-run the check: every pixel must give cream `#FAF4EB` 5.0:1 or better.
- Native picks `board.webp` / `@2x` / `@3x` by screen scale. iOS 14+ decodes WebP through ImageIO; if RN's
  `resizeMode="repeat"` misbehaves with WebP on a device, ship the same tiles as PNG (`board@3x.png` ~ 3-4x heavier).

## 2. One shared texture source (Header + Rail)

New `src/kit/layer/boardTexture.native.ts` / `boardTexture.web.ts`:

```ts
// boardTexture.native.ts
export const HEADER_BOARD = require('../../../assets/brand/board.webp'); // Metro adds @2x/@3x
// boardTexture.web.ts
export const HEADER_BOARD = {
  x1: require('../../../assets/brand/web/board-1x.webp'),
  x2: require('../../../assets/brand/web/board-2x.webp'),
  x3: require('../../../assets/brand/web/board-3x.webp'),
};
export const BOARD_TILE = { width: 1440, height: 140 } as const; // in both files (or a shared .ts)
```

- `src/components/Header.tsx`: `BOARD_VARIANTS = [{ id: 'n-r8-01', texture: HEADER_BOARD }]` (one board; add rows only
  if Tyler wants the day set: `tiles/N-r8-04`, `N-r8-05`, 341 KB for all three).
- `src/kit/frame/Rail.tsx` line 29: `const BOARD_TEXTURE = require('.../endgrain-bp.svg')` → `import { HEADER_BOARD }`
  (and take today's variant through `useBoardVariant()` if a day set ships), so the rail strip and the bar can never
  show two different boards.

## 3. `src/kit/layer/TopInsetBoard.tsx`

Web (`webTileStyle`):

```ts
const uri = (a: unknown) => (typeof a === 'string' ? a : (a as { uri?: string } | null)?.uri ?? null);
export function webTileStyle(t: Texture): ViewStyle | null {
  const set = t as unknown as { x1?: unknown; x2?: unknown; x3?: unknown };
  const u1 = uri(set.x1), u2 = uri(set.x2), u3 = uri(set.x3);
  if (!u1 || !u2 || !u3) return null;                  // flat bg-header shows: honest degradation
  return {
    backgroundImage: `image-set(url("${u1}") 1x, url("${u2}") 2x, url("${u3}") 3x)`,
    backgroundSize: '1440px 140px',                    // FIXED CSS size: blocks are 36 px on every screen
    backgroundPosition: 'left bottom',                 // anchored to the BAR's bottom: two whole rows in the 56 row
    backgroundRepeat: 'repeat',
  } as unknown as ViewStyle;
}
```

- `image-set()` unprefixed: Chrome 113+, Safari 17+, Firefox 88+. Older browsers get the flat `bg-header` brown.
- A browser downloads ONE file: 15 KB (1x screen), 37 KB (2x), 61 KB (3x phone).

Native (replaces `<ExpoImage contentFit="cover">`):

```tsx
import { Image } from 'react-native';
<Image
  source={texture}
  resizeMode="repeat"
  style={{ position: 'absolute', left: 0, right: 0, bottom: 0, height: BOARD_TILE.height }}
/>
```

- The tile repeats from the Image view's top-left; with `bottom: 0, height: 140` its rows line up with the bar's
  bottom exactly like web. The board view keeps `overflow: 'hidden'` (NATIVE_CLIP). The tallest bar is 59 + 56 = 115,
  under 140; if a bar is ever taller, use a height that is a multiple of 140.
- Check on an iPhone (3x) and an iPad (2x): blocks must be 36 pt, rows whole at the bottom, no seam every 1440.

The 1 px rule (DESIGN 2.8.4: a line, not a shadow): a child `View` at the board's bottom,
`{ position: 'absolute', left: 0, right: 0, bottom: 0, height: 1 }` with class `bg-header-rule`.

## 4. Tokens (`src/kit/palettes/light.js`)

- Add `'header-rule': 'rgba(20,8,0,0.55)'` (the bar's bottom line).
- The mark tile needs NO new colour: it is `#FAF4EB` = `header-text`, carried by the icon file itself.
- `header` #6B3E14 stays the base colour (the flat fallback). The board's average in the 56 row is now #6E4019.

## 5. Frame and type

- `src/kit/frame/metrics.ts`: `headerRow: 50` → `56` (comment: "two whole 28 rows of the board tile").
  `AppFrame.test.tsx` reads `FRAME.headerRow`, so it follows. Onboarding / welcome headers (58 today) use
  `FRAME.headerRow` too.
- `frameHeaderLead()` stays (8 beside the wide rail, 10 beside the slim rail); the mark's left edge sits there. Phone:
  `SHELL_GUTTER` 16.
- Header row right padding: 16 → 8 (header only), so the avatar circle's edge sits ~16 from the screen edge, like
  the mark on the left.
- `src/kit/scales.js` `wordmark.header`: 22 → 24; `Wordmark.tsx` weight 600 → 700, letterSpacing -0.24
  (-1%). Native needs the face, which the app does NOT ship today (`assets/fonts` has 700Bold but no 700 italic):
  add `IBMPlexSans_700Bold_Italic.ttf` (IBM Plex Sans, OFL, same source as the others) to `assets/fonts` and the
  expo-font list in `app.json`, and use `fontFamily: 'IBMPlexSans-BoldItalic'`. Web: the variable italic face already
  draws 700.
- `PrimaryHeader.tsx`: inside the `primary-logo` ShellAction, before `<Wordmark>`: the 26x26 `sc-mark.svg` + an 8 gap
  (decorative: `accessible={false}`; the link already says "SupperCraft home").
- Bar text does not grow with system text size: pass `maxFontSizeMultiplier={1}` on the wordmark, timer and
  "Sign in" (the menu and screen readers carry the full words).

## 6. Status slot rule (when E7b saving and E10b timer are built)

When the room between the name and the right side is under 12: (1) a timer of 1 hour or more takes its short form
("1h 4m"); (2) the timer shows only its icon; (3) the saving cloud moves onto the avatar as a tiny cream cloud
(17x13, brown 2.2 edge, top-right). Mark and name never change. Screen readers always hear "Saving" and the full time.

## 7. Pages

- Sign-in (`app/sign-in.tsx`): bar only, nothing top right, NO second big wordmark (today it has none: keep it so).
  `about.tsx` and `invite/[token].tsx` still use `Wordmark size="signIn"` (28): Tyler's call whether 2.5.6 keeps a
  second size for them.
- Signed-out pages that have one: a real "Sign in" button top right (44 target). Shopper link: nothing top right
  (no "Shared list" label in the bar; the page says it). There is no "Shared list" in the code today: just do not add it.
- Avatar: no change. `Avatar.tsx` with `ring` already draws one 1.5 cream border and no dark outline. Optional
  (Tyler): make the DERIVED default colour (someone who never picked one, `derivedDisplayColor`) come from the warm
  deep colours only (Brick, Copper, Moss, Plum, Raspberry) so a new account never starts cold on the wood.

## 8. Tests

- `src/kit/layer/__tests__/layer.headerTopInset.test.tsx` line 20 expects `backgroundSize: '720px 108px'` →
  expect `'1440px 140px'`, `backgroundPosition: 'left bottom'`, and `backgroundImage` starting `image-set(`; add a case
  where one of x1/x2/x3 has no URI → `null`.
- Native test: `TopInsetBoard` renders an `Image` with `resizeMode="repeat"`, `bottom: 0`, `height: 140`.
- Rail test: the rail strip's texture is `HEADER_BOARD` (same object as Header's).

## 9. DESIGN.md (change in the same work)

- 2.5 table, wordmark row: "22 in the header, 28 on sign-in, italic" → "24 bold italic in the header".
- 2.5.6: "One Wordmark component, two sizes: 22 header, 28 sign-in" → "One Wordmark, 24 bold italic, in the header
  bar. Sign-in shows no second wordmark (the bar already says it)." (+ Tyler's call on about / invite.)
- 4.1.1: "...a texture that varies by day" → "...one board everywhere (N-r8-01): a 1440x140 tile, 36 px blocks, drawn at
  that fixed size and anchored to the bar's bottom on iPhone, iPad and web." (Keep "varies by day" only if Tyler
  picks the day set.)
- 4.1.4: "member colour with a bolder outline and a thin cream ring" → "member colour with one thin cream ring" (what
  the code already does).
- New 4.1.7: "The bar row is 56 (two whole board rows) on every page and size, plus the status-bar inset. Left: the SC
  mark (the app-icon tile, 26) then the wordmark, starting at the frame lead. Right: the status slot, then the account
  (or a 'Sign in' button signed out). Words in the right corner are always tappable. It ends in a 1 px `header-rule`
  line, never a shadow."
- New 4.1.8: the narrow-phone rule in section 6 above.

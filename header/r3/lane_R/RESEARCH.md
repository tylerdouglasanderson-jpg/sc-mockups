# I-007 lane R: research on the SupperCraft header bar

Read-only research, 2026-11-27. Code read at `C:/mise-rebuild/app` (working tree as of today).

**Source warning.** This session had no web-search tool. Sections 1 and 6 (SupperCraft code) are checked
against the code line by line. Sections 2, 3 and 5 (other apps, platform rules, brands) come from what I
already know (up to mid-2026), not from pages loaded today. Numbers marked "about" are close, not
measured. Before any of them goes into DESIGN.md, a builder with a browser should check them (open the
site, measure the bar in dev tools; check the cited guideline pages).

---

## 1. What the header holds today

### 1.1 The main bar (`PrimaryHeader`) - the one most pages show

Code: `src/components/PrimaryHeader.tsx`, `src/components/Header.tsx`, `src/kit/layer/TopInsetBoard.tsx`,
`src/kit/frame/metrics.ts`, `src/kit/Wordmark.tsx`, `src/kit/Avatar.tsx`.

| Part | What it is today | Where in code |
|---|---|---|
| Height | **50** (pt / px) row, every platform (`FRAME.headerRow: 50`, "was 58", T-1000/T-1005). On iPhone and iPad the board also runs up under the status bar, so the brown area is 50 + the top inset (about 47-62 pt on a modern iPhone, 24 on iPad). | `metrics.ts:26`, `PrimaryHeader.tsx` `style={{ height: FRAME.headerRow }}` |
| Background | Brown `#6B3E14` (token `header`) under an end-grain SVG, `endgrain-bp.svg` 720x108, 18 px blocks, 3 colours (`#6B3E14` x86, `#8A5828` x85, `#7A4A1E` x69). Web tiles it at 720x108. Native stretches it to cover (expo-image `contentFit="cover"`). One day-variant only (`BOARD_VARIANTS`). | `Header.tsx`, `TopInsetBoard.tsx` |
| Left | Wordmark "SupperCraft", IBM Plex Sans **SemiBold Italic (600)**, **22** size, line height 26, cream `#FAF4EB`. It is a link to Home (`goToTab`). 32 px space after it (`pr-8`). No mark / no SC tile. | `Wordmark.tsx`, `scales.js:61` |
| Middle | Nothing. Page words and section links were taken out of the bar (D7 A, lint `D7-header-nav`). | `PrimaryHeader.tsx` header comment |
| Right, before avatar | A "status slot": the saving cloud (only lit while something waits to save) and a timer place that is still empty. Fixed places so the bar never shifts. | `HEADER_STATUS_SLOTS` |
| Right | The account button: the person's avatar, **29** circle in their own colour, thin cream ring, inside a 44 tap square. Grows 6% on hover (web). Opens the account menu: Settings, Household, History, About SupperCraft, Help, Report a Problem, My Reports, (staff: Ticket Workbench, Folders look), Sign Out of This Device. | `Avatar.tsx` (`AVATAR.header = sm = 29`), `PrimaryHeader.tsx` |
| Scroll | Never shrinks or moves. (DESIGN 4.1.3's "turns light tan on scroll" is about the tan bar below, not the board.) | - |

Contrast of the cream words on the board: 8.3:1 on the base brown, **5.5:1 on the lightest block
`#8A5828`**, 6.8:1 on the middle one. All pass 4.5:1 today, but the lightest block leaves little room: a
lighter species (maple, cherry) in a new board would fail behind the wordmark unless something calms
that spot.

### 1.2 Per platform

| Platform | Who draws the bar | Brown height | Left edge of the wordmark |
|---|---|---|---|
| Web wide (700 px and up, wide rail 220) | The frame draws ONE bar across the full width, above the rail and the page (T-1130). | 50 | Lined up with the rail's items (`frameLead`). |
| Web narrow (under 700, phone layout) | Each screen draws its own `PrimaryHeader`. Bottom tabs. | 50 | Page padding. |
| iPhone | Each screen's own `PrimaryHeader`; board runs under the status bar. Bottom tabs. | inset + 50 (about 109 on an iPhone 15/16) | Page padding. |
| iPad upright (slim rail 64) | Frame draws one bar across the top, under the status bar. | 24 + 50 | Over the slim rail. |
| iPad sideways (wide rail 220) | Same as above. | 24 + 50 | Over the wide rail. |
| Kitchen iPad, Home "at rest" | **No brown bar at all.** The rest screen (`KitchenRestGate`) shows the date and big cards. | 0 | - |
| Kitchen iPad, other states | `PrimaryHeader` (no rail: kitchen has no frame chrome). | 24 + 50 | Page padding. |

### 1.3 Every drift from "same height, same background, same logo"

| # | Screen(s) | What differs | Code |
|---|---|---|---|
| D1 | Sign-in, sign-up, check email, confirm, forgot / reset password, auth finish, invite (wide layout) | Bar is **44** (the bare `Header` default class `h-hdr-landscape` = 44 px), wordmark 22, no avatar. | `EntryShell.tsx:149`, `tailwind.config.js:87` |
| D2 | Same auth screens, narrow / story layout | Bar is **auto height, at least 58**, wordmark **28** (the sign-in size) on the bar, plus a note in the bar on tablet / computer. | `EntryShell.tsx:291-293` |
| D3 | Welcome, onboarding | **58** (`EntryHeader`, `ENTRY_SIZE.storyHeader`), wordmark + ringed avatar. | `EntryParts.tsx:56,289` |
| D4 | Inventory setup | **58** hard-coded, wordmark 22. | `SetupChrome.tsx:23` |
| D5 | Shopper link (`/shop/[token]`, signed-out shopper) | **58**, wordmark 22, plus the words "Shared shopping list" on the right (only header with words besides the wordmark). | `ShopParts.tsx:164,203`, `app/shop/[token].tsx:45-49` |
| D6 | Cook | **No brown bar**: a light tan band with "Leave" and the recipe name (on purpose, DESIGN 8.1.2). | `CookChrome.tsx` `CookHeader` |
| D7 | Kitchen iPad at rest | **No brown bar.** | `app/index.tsx` kitchen branch |
| D8 | Native vs web board | Web tiles at 720x108 (blocks stay 18 px). Native "cover" scales one 720x108 picture to the bar's size, so on a wide iPad the blocks grow (about 1.6x at 1180 wide) and on a phone the image is cropped. Same file, different look. | `TopInsetBoard.tsx` |
| D9 | Brand files | `logo-lockup-header.svg` and the SC tile files exist but nothing in the app uses them; the bar shows text only. README calls the SC mark temporary. | `assets/brand/README.md` |
| D10 | Leftover tokens / notes | `hdr-portrait: 54px` is defined but nothing uses it. `Wordmark.tsx` still says "NOT SWEPT: PrimaryHeader ... draw their own wordmark text", which is no longer true (PrimaryHeader uses the kit Wordmark). | `tailwind.config.js:88`, `Wordmark.tsx` |

So today there are **four header heights** (44, 50, 58, auto-58+), **two wordmark sizes on the bar**
(22, 28), and **two screens with no board**. The signed-in app proper (Today, Plan, Recipes, Shop,
Kitchen, Capture, History, Settings, Notifications, Recipe, Prep, Leftovers, Import) is already
consistent at 50 with the same three parts.

---

## 2. What other apps do

Not re-measured today (see the warning at the top). "Phone" = the iOS app unless noted.

| App | Phone header | Desktop / web header | What sits in it | Shrinks on scroll? |
|---|---|---|---|---|
| **Paprika** | Standard iOS bar 44 + page title ("Recipes"); add (+), sync, edit buttons. | Mac app toolbar about 52 with search. | Page title, +, search, no logo. | iOS large titles collapse. |
| **Mealime** | Page title only, simple bar; bottom tabs. | Web: logo left, links, account, about 64-72. | Title; logo only on web. | Phone title collapses. |
| **NYT Cooking** | Logo (the NYT "T" mark + "Cooking") at top of the home feed, search, profile; bottom tabs. | About 60-64: logo left, search, "Your Recipe Box", account right. | Mark + wordmark, search, saved box, account. | Web bar sticks; app logo scrolls away. |
| **Plan to Eat** | Simple page title. | About 56-64: logo left, Recipes / Planner / Shopping links, account right. | Logo, main nav, account. | No. |
| **AnyList** | iOS large titles (list name), share and + buttons. | Mac / web toolbar. | Title, share, add. No logo. | Large title collapses. |
| **Samsung Food** (was Whisk) | Search box on top, avatar, notifications. | About 64: logo, search, + (create), notifications, avatar. | Logo, search, add, bell, avatar. | No. |
| **Crouton** | iOS large titles, very plain. | Mac. | Title, +. No logo. | Collapses. |
| **Notion** | 44: back, page name, share, "...". | About 45: breadcrumb (page path), Share, comments, star, "...". Workspace switcher sits at the top of the sidebar, not the bar. | Page path + page tools. No logo in the bar. | No. |
| **Linear** | 44-ish nav bar. | No global bar. Sidebar top holds workspace switcher, search, new issue. Page header about 44-50 with the view name. | Workspace switcher, search, quick add, page name. | No. |
| **Airbnb** | No logo; a big search pill at top; bottom tabs. | About 80: logo mark + wordmark left, search pill centre, "Airbnb your home", globe, menu + avatar pill right. | Logo, search, host link, language, account. | Yes: the big search folds into a slim one when you scroll. |
| **Things 3** | Large title per list (44 bar + title), collapses. | Mac: no bar; title inside the page. | Title. No logo, no account. | Title collapses. |
| **Spotify** | No logo. Avatar top left + filter chips (Music, Podcasts). | About 64: home button, big search in the middle, notifications, friends, avatar right. | Home, search, bell, avatar. | No (page colour fades in under it). |
| **Gmail / Google apps** | Search pill with avatar inside it. | 64: menu, logo, search, help, settings, apps grid, **avatar top right**. | Logo, search, account. | No. |
| **YouTube** | 48-56: logo left, cast, bell, search. | 56: menu, logo, search, create (+), bell, avatar. | Logo, search, add, bell, account. | Phone hides on scroll down. |
| **Apple apps** (Music, App Store, Photos, Notes) | Large title (96 with title) collapsing to 44; **App Store and Music put the account picture top right** in the large title. | Mac: toolbar 52 with sidebar. | Page title, account (App Store / Music), +. No logo ever. | Yes, large title collapses. |

What this says:

- **Account top right is near universal** (Google, YouTube, Airbnb, Spotify, Samsung Food, Apple App
  Store, NYT Cooking). SupperCraft already does this. Keep it.
- **A logo in a phone header is rare** for apps you already opened (Apple, Things, Notion, Spotify, Airbnb
  show none). Brands that do show one are content or media brands (NYT Cooking, YouTube). SupperCraft
  showing the wordmark on every page is a brand choice, like the cutting board itself. It is fine, but it
  is the opposite of what most phone apps do, so it should earn its space (small, calm, tappable to Home).
- **Desktop web headers carry the logo almost always**, logo far left.
- **Search is the most common extra** (Samsung Food, NYT Cooking, Airbnb, Spotify, Google, YouTube).
  DESIGN 4.1.2 says search lives elsewhere.
- **Quick add (+)** appears on creation-heavy apps (Samsung Food, YouTube, Linear). SupperCraft's "+" is
  Capture, already in the tab bar / rail.
- **Shrinking on scroll** is common on iOS (large titles) and on Airbnb, but those bars START tall. A short
  bar (44-64) almost never shrinks.

---

## 3. Platform norms

| Platform | Norm | Source |
|---|---|---|
| iOS (iPhone) | Standard navigation bar **44 pt**; large-title bar **96 pt** (44 + 52 title), collapsing to 44 on scroll. Tab bar 49 (+34 home indicator). Status bar about 47-62 pt on notch / Dynamic Island phones (not counted in the 44). Min tap target 44x44. | Apple Human Interface Guidelines, "Navigation bars" and "Layout" (developer.apple.com/design/human-interface-guidelines/navigation-bars); `UINavigationBar` docs |
| iPadOS | Navigation bar **50 pt** (since iPadOS 13); status bar 24. | Same HIG pages; measured in Xcode simulator by many |
| Android (Material 3) | Small / centre top app bar **64 dp**; medium **112 dp**; large **152 dp** (medium and large collapse to 64 on scroll). | m3.material.io/components/top-app-bar/specs |
| Android (Material 2, older) | **56 dp** phone, **64 dp** tablet / desktop, 48 dp dense. | m2.material.io/components/app-bars-top |
| Web apps | Mostly **48-72 px**. Examples: Notion about 45, YouTube 56, GitHub about 64, Gmail 64, Spotify about 64, Airbnb about 80. | Measured by design blogs; re-measure before quoting |

SupperCraft's 50 sits between iOS's 44 and Material's 56 / 64. It equals iPadOS's 50 exactly.

---

## 4. What else could go on the header

Ranked best first. "Who" = which household member gains.

| Rank | Idea | Who uses it | For | Against | Pick |
|---|---|---|---|---|---|
| 1 | **SC mark left of the wordmark** (the favicon tile, small) | Everyone; new users learning the brand | Ties the app icon to the app; makes the brand read at a glance; most desktop headers pair mark + name; a mark alone can stand in on very narrow screens. | The mark is called temporary (brand README); a cream tile on brown adds a bright square that pulls the eye. | **Yes, try it** (lane L). Try both the cream tile and a "burned in" brown-on-brown version. |
| 2 | **Sync / offline sign** (already there: saving cloud) | Shopper in a store with weak signal; kitchen tablet | Honest about unsaved work; already built, takes no room when idle. | None while it stays quiet. | **Keep as is.** |
| 3 | **Running timer** (slot already reserved) | The cook, while away from Cook | One look tells "the rice has 4 minutes". Apple shows timers in the Dynamic Island the same way. | Only matters while cooking. | **Keep the slot; build when timers are built.** |
| 4 | **Today's date / meal of the moment** ("Thu 27 · Dinner: Tacos") | Kitchen tablet; morning planner | Glanceable; fits the kitchen-board feel. | Today page already shows the date in the grey bar under the header; repeats it; words on wood are harder to read. | **Kitchen iPad only, if at all** (and that screen has no header at rest today). |
| 5 | **Notifications bell** | Household members waiting for plan approval | Common pattern; there is already a Notifications page. | "No tab badges for now" (3.5.5) leans against dots; adds a second round button next to the avatar. | **Not now.** Put a Notifications row in the avatar menu if it is hard to find. |
| 6 | **Household switcher** | People in two households (rare) | Notion / Linear / Slack do this. | Most people have one kitchen; adds a menu nobody opens. | **No**; the avatar menu's Household row covers it. |
| 7 | **Search** | Recipe hunters on desktop | The most common extra on other apps. | DESIGN 4.1.2 rules search out of the bar; search lives on Recipes. | **No** (unless Tyler wants app-wide search later). |
| 8 | **Quick add (+)** | Everyone | One tap to Capture. | Capture already sits in the tab bar (phone) and at the rail top (iPad / web). Two "+" buttons is noise. | **No.** |
| 9 | **Page title on the bar** | Everyone | iOS does this. | Removed on purpose (D7 A); the tan bar below carries the page name on scroll. | **No.** |

The bar's job stays: **brand left, quiet status middle-right, account right.** Fewer things done well.

---

## 5. Wordmark and mark

### How food and craft brands set their names (from memory, check before quoting)

| Brand | Wordmark style | Mark beside it? |
|---|---|---|
| NYT Cooking | Blackletter "T" mark + clean sans "Cooking" | Yes, mark left |
| Bon Appétit | Bold serif-ish display | No |
| Food52 | Lowercase sans, friendly | No |
| Serious Eats | Bold sans | No |
| HelloFresh | Heavy rounded sans | Lime leaf mark |
| Blue Apron | Sans, with an apron / bird mark at times | Sometimes |
| Le Creuset | Classic serif | No |
| Etsy | Warm slab-ish serif, orange | No |
| Mailchimp | Soft rounded serif (Cooper-like) | Freddie mark left |
| Field Notes, Filson | Craft brands: condensed sans or serif, often "stamped" | Badge style |

Patterns:
- **Craft and kitchen warmth** usually comes from a **soft serif or a humanist italic**. SupperCraft's
  semibold italic sans is in the humanist lane already. DESIGN 2.5.5 bans serifs everywhere; a serif
  wordmark would need Tyler to make the logo an exception (logos are often treated as pictures, not type).
- **Weight**: brand names on dark bars are usually **semibold to bold** (600-700). 600 italic at 22 is on the
  light side on a busy wood texture.
- **Letter spacing**: italics and bold display names usually tighten slightly (-1 to -2 %). Plex italic at
  default spacing can look loose at 22.
- **Mark left of the name**: the norm on desktop (Airbnb, NYT Cooking, Mailchimp, Slack, Linear). Size the
  mark to about the cap height + a bit (for a 22 wordmark, a 24-28 tile), with a gap about half the mark.
- **Two-tone names** ("Supper" + "Craft" in two weights) are common for compound names and help the
  eye split it; risk is it reads as two words. Worth a variant in lane L.

### Making it stand out on wood

Ranked by calm-ness:
1. **A calm patch**: the board under the wordmark is smoother, darker or a single long-grain plank (like a
   branded tag or an inlay). Keeps the board everywhere else. Best fit with "cutting board" and fixes the
   5.5:1 worst case. Lanes A/B should design this patch into the board, not paste a box on top.
2. **More weight / size**: 22 -> 24, 600 -> 700. Cheap and honest.
3. **A soft dark shadow** (about 0 1 2 at 30-40 % brown): very common for text on photos. DESIGN 2.8.4 bans
   decorative shadows; a legibility shadow is arguably not decorative, but Tyler should rule.
4. **"Burned in" look** (the name looks branded into the wood, darker brown with a light edge): striking,
   on theme, but lower contrast and hard to read small. Good for the sign-in hero, risky for the bar.
5. **Outline / stroke**: looks cheap at this size. Skip.

---

## 6. Height

Tyler's rule: always the same height.

**Recommendation: one row height, 56, on every platform and every screen that has the board.**
(iPhone and iPad add the status-bar inset above it, like today; the row itself is 56.)

Why 56 rather than today's 50:
- It is the Material phone bar and YouTube's bar; it sits mid-way between iOS (44) and desktop web (64).
- It holds the 44 tap targets with 6 above and below (today 3). The menu-open and hover-grow already
  need that room.
- It gives the board more wood to show (the whole theme), and room for a 26-28 SC mark beside a 22-24
  wordmark without looking cramped.
- It is 6 pt more on a phone. With the status bar the phone header goes from about 109 to about 115,
  still well under iOS's 140+ for a large title.
- It retires the 44 / 50 / 58 / auto mix with one number that is closer to the 58 the auth and setup
  screens already chose.

If Tyler wants the phone to keep every pixel: **keep 50 everywhere** instead. 50 also works; the main
point is ONE number in ONE token (`FRAME.headerRow`), and every `Header` user reads it (no hard-coded
44 / 58, no `height: 'auto'`).

Should it ever vary?
- **Shrink on scroll: no.** The bar is already short; shrinking only pays when a bar starts tall (iOS
  large titles, Airbnb). It would also break Tyler's rule and the rail-strip line-up on iPad / web.
- **Bigger on sign-in: no** for the bar. Put the large 28 wordmark in the page body (as the narrow
  sign-in card already does), keep the bar the same.
- **Cook: keep the exception** (tan band, no board). Cook is true full screen by design (3.5.3, 8.1.2);
  hiding the brand while cooking is right. Ask Tyler to confirm it is an allowed exception.
- **Kitchen iPad at rest: ask.** It has no board today. Showing the bar there would make the kitchen
  tablet feel like the same app from across the room.
- **Large text (150 %+)**: the bar can stay 56; the wordmark is a logo and need not grow with text size
  (Apple does not scale its bar titles past a point either).

Also fix D8: native should draw the board at the same block size as web (tile, or a picture made at the
bar's real size), so "same background" is true on iPad as well as web.

---

## Questions worth asking Tyler

1. **One height: 56 or keep 50?** Pick: **56** - more wood, room for the mark, 6 pt margin round the 44
   targets; one token everywhere.
2. **Should sign-in, welcome, onboarding, setup and the shopper link use the same bar as the app (today
   44 / 58 / auto)?** Pick: **yes** - that is the "same height, same logo" rule; the big wordmark moves
   into the page.
3. **Cook keeps its tan band, no board?** Pick: **yes** - Cook is full screen on purpose.
4. **Kitchen iPad at rest: add the bar?** Pick: **yes** - same app at a glance from across the kitchen;
   it costs 74 pt on a big screen.
5. **Add the SC mark left of "SupperCraft"?** Pick: **yes, try it** - pairs the app icon with the name;
   but the mark is marked temporary, so the bar should not lock its look in.
6. **May the wordmark get a calm patch of board, heavier weight (700), or a soft shadow to stand out?**
   Pick: **calm patch + 700 weight; no shadow** - on theme, and avoids the decorative-shadow rule.
7. **Is the wordmark a logo (so serif or a custom lettering is allowed), or type (so the no-serif rule
   holds)?** Pick: **logo** - lets lane L try a warmer, more "craft" lettering without changing app type.
8. **Anything new on the bar?** Pick: **no new buttons**; keep saving cloud, fill the timer slot when
   timers exist; maybe a Notifications row in the avatar menu.
9. **"SupperCraft" one word, or two-tone "Supper" + "Craft"?** Pick: **one word, one colour** - the name
   is one word everywhere else; try two-tone only as a lane L variant.

## Summary

The signed-in app already has one header: 50 tall, end-grain board, "SupperCraft" in 22 semibold italic
Plex, a quiet saving cloud, and the account picture top right. The drift is outside it: auth screens at
44 or 58+ with a 28 wordmark, welcome / onboarding / setup / shopper link at 58, no board in Cook or on
the kitchen tablet at rest, and the board drawn bigger on native iPad than on web. Other apps put the
account top right (same as ours), rarely put a logo in a phone bar, and keep short bars fixed. Best next
moves: one height (56, or 50) in one token for every board screen, a small SC mark beside a slightly
heavier wordmark, a calm patch of wood behind the name instead of a shadow, and no new buttons.

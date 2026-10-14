# pallas-design-tokens

Single source of truth for Pallas's color/radius/font-size design tokens
(`design-tokens.json`). Public so both consumers can install it as a plain
git dependency with no auth:

- `pallas` (private app repo) — `universal/tailwind.config.js` and the
  transactional email templates in `server/services/emails/`.
- `pallas-marketing-site` — generates its CSS custom properties from the
  same values, see that repo's `scripts/src/generate-tokens.ts`.

To change a token: edit `design-tokens.json` here, commit, push, then in
each consuming repo run `npm update pallas-design-tokens` (or `pnpm update
pallas-design-tokens` in pallas-marketing-site) to pick up the new commit —
a plain `install` reuses whatever commit is already recorded in the
lockfile and won't refetch on its own.

## Gold on light, peach on navy

There are two accent tokens — `secondary` (gold, `#916d09`) and `accent`
(peach, `#ffcaa8`) — and which one to use depends on the surface behind
it, not preference. Gold text on a navy (`foreground`) surface is ~3:1
contrast, too low to read — that's the bug this rule prevents.

| Role | On white / muted | On navy surfaces |
|---|---|---|
| Body text | `foreground` | white (`secondaryForeground`) |
| Secondary text | `mutedForeground` | white (`secondaryForeground`) |
| Eyebrows / numbers (label role) | `mutedForeground` on light, `foreground` + bold for numbers — weight and letter-spacing signal "label," not color | `accent` (peach) stays the decorative color here |
| Links (actually interactive) | `secondary` (gold) | `accent` (peach) |
| Primary button | `secondary` bg + white text | `accent` bg + `foreground` text |
| Light sections, top bar, banner | `muted` | n/a |

Eyebrows and numbers are a label, not a link — on light surfaces they
don't get an accent color at all (`mutedForeground` for eyebrows,
`foreground` bold for numbers like 01/02/03). On navy surfaces peach
still carries them, since there's no gray token light enough to read
there. Exactly because peach does double duty on navy (decorative label
*and* interactive accent), any genuinely clickable element on a navy
surface must look like a button (filled `accent` bg + `foreground`
text) — never a bare peach text link, which would be indistinguishable
from a label.

Exceptions:
- Filled badge/chip components (e.g. the oxalate badge) can always use
  `accent` bg + `foreground` text regardless of the surface they sit on —
  the chip supplies its own contrast, so it doesn't need to switch tokens.
- Border and muted-gray tokens don't change with surface — they're
  already in the same navy-derived hue, so they read fine on both.
- Decorative, meaning-coded color coding (e.g. a chart legend where gold
  and peach each represent a different data series, not "accent on this
  surface") isn't this rule — don't force those to switch per surface.

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

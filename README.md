# pallas-design-tokens

Public mirror of `shared/design-tokens.json` from the private `pallas` app repo.

`pallas` remains the single source of truth for these values (it's also consumed
directly by `universal/tailwind.config.js` there). This repo exists only so that
`pallas-marketing-site` can install it as a git dependency without needing
credentials for a second private repo — see that repo's
`scripts/src/generate-tokens.ts`.

**To update**: copy the latest `shared/design-tokens.json` from `pallas` over the
one here, commit, and push. There's no automated sync yet.

# snapseq

Playwright Test fixture package for scripted screenshot captures. One package at the repo
root; consumers install it into their own app and keep all business logic there.

- Install: `pnpm install` (builds `dist/` via `prepare`), then `pnpm exec playwright install chromium`
  under Node 20 or 22 (`playwright install` hangs under Node 26; `nvm use 22` first).
- Test: `pnpm test` (builds, then 3 files; the integration file launches real Chromium).
- Typecheck: `pnpm typecheck`.
- Keep it tiny: no brand selectors, no site-specific helpers, no exports without a real consumer.
- `docs/` is the API reference and `README.md` the front door; update them with any public change.

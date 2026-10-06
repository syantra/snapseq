# snapseq

Playwright Test fixtures for scripted screenshot captures. A capture is a
Playwright test; snapseq adds numbered screenshots per run, capture and
device, env and host selection, one project per device, a `snapseq`
command, and defaults suited to long sequential runs. Everything else is stock
Playwright: `--headed`, `--ui`, `--debug`, `--trace on`, reporters, the VS Code
extension.

## Quick start

In the app that owns the pages:

```bash
pnpm add -D @playwright/test "snapseq@github:syantra/snapseq#v0.1.0"
pnpm exec playwright install chromium   # once per machine; under Node 26 run this with Node 22
```

```ts
// snapseq.config.ts
import { defineSnapseq } from "snapseq";

export default defineSnapseq({
  envs: { dev: { host: "http://localhost:3000" } },
});
```

```ts
// captures/pricing.capture.ts
import { capture, disableTransitions } from "snapseq";

capture(async ({ page, seq }) => {
  await disableTransitions(page);
  await page.goto("/pricing");
  await seq.snap();      // 001.png  the viewport
  await seq.snapPage();  // 002.png  the whole page
});
```

```bash
pnpm screenshot   # "screenshot": "snapseq" in package.json
```

```
.screenshots/2026-10-01 at 4.07.16 PM/pricing/desktop/001.png
.screenshots/2026-10-01 at 4.07.16 PM/pricing/desktop/002.png
.screenshots/2026-10-01 at 4.07.16 PM/pricing/mobile/001.png
.screenshots/2026-10-01 at 4.07.16 PM/pricing/mobile/002.png
```

## Docs

| Page                                        | Answers                                                              |
| ------------------------------------------- | -------------------------------------------------------------------- |
| [Getting started](docs/getting-started.md) | How do I get from an empty app to a PNG?                             |
| [Config](docs/config.md)                   | How do I set up envs, devices, the dev server, Playwright options?   |
| [Captures](docs/captures.md)               | How do I write a capture that takes the right shot?                  |
| [Running](docs/running.md)                 | How do I run it, and what do the outputs and the terminal mean?      |
| [Examples](docs/examples.md)               | Complete capture files, basic to complex.                            |
| [Troubleshooting](docs/troubleshooting.md) | Something looks wrong.                                               |

## Develop and release

```bash
pnpm install          # also builds dist/ via prepare
pnpm typecheck
pnpm test             # builds, then unit + integration tests (real Chromium)
git tag v0.1.0 && git push origin HEAD v0.1.0
```

Consumers bump the tag in their `package.json`. `docs/` is the API reference;
a public change updates it.

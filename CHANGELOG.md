# snapseq

## 0.1.0

### Minor Changes

- Initial release. Playwright Test fixtures for scripted screenshot captures.
  - `capture()` files write numbered PNGs per run, capture and device, with `shots.txt` listing each file's URL.
  - `seq.snap()` for the viewport and `seq.snapPage()` for the whole page; both wait for the DOM to go quiet, fonts and images, and note on the shot when a wait ran out.
  - `defineConfig()` with envs and hosts, HTTP credentials scoped to the host's origin, per-env Playwright `use` options, a dev server command, one project per device, and Playwright overrides as extra arguments.
  - The `snapseq` command with `--env`, `--host` and `--device`; everything else goes to `playwright test`.
  - A live terminal view for interactive runs, `failed.png` beside the shots when a capture dies, and a run directory per run.

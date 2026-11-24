# opencode-magnific

OpenCode / magpie plugin exposing Magnific image and video generation as tools. See README.md.

- Test: `bun test` (uses a local stand-in for api.magnific.com; no key, no credits).
- Regenerate the model catalog: `bun run catalog` (never edit `catalog.json` by hand).
- `index.mjs` must export the plugin function and nothing else: hosts call every export as a plugin.
- Try it in a throwaway magpie (does not touch the real one):
  `sb=$(mktemp -d); m() { env HOME=$sb XDG_CONFIG_HOME=$sb/.config XDG_CACHE_HOME=$sb/.cache MAGPIE_ADDR=127.0.0.1:3499 magpie "$@"; }; m plugin add "$PWD" </dev/null; m plugin --json`
  Tool calls go through `magpie web --no-open --gateway --addr 127.0.0.1:3497` in that sandbox, at `http://127.0.0.1:3499/mcp/magpie/tools`.
- One tool call may run 55 seconds at most under magpie; keep waits at or below 50.
- The same files live in magpie-community/plugins as `packages/magnific-api` (`@magpie-community/magpie-magnific-api`, no dependencies). A change here is copied there, with its version bump.
- Publishing to npm (`npm publish --access public`) needs the owner's 2FA in a browser.

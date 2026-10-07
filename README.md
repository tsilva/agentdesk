<p align="center">
  <img src="https://raw.githubusercontent.com/tsilva/claudesk/main/logo.png" alt="maestro" width="512" />
  <br />
  <!-- repo-tagline:start -->
  <strong>🖥️ Interactive dashboard for launching and managing OpenCode agents ⚡</strong>
  <!-- repo-tagline:end -->
</p>

🖥️ **Interactive dashboard for launching and managing OpenCode agents** ⚡

maestro is a local web dashboard for running OpenCode agents across your git repositories. It gives you one browser tab for creating sessions, sending follow-up prompts, approving tool permissions, watching live output, and tracking token and cost totals.

The app runs as a Bun + Hono server with server-rendered HTML, HTMX partial updates, and SSE for real-time agent streams.

## Install

Use Bun **1.3.14**, pinned in `package.json`, with the committed `bun.lock`.

```bash
git clone https://github.com/tsilva/claudesk.git
cd claudesk
bun install --frozen-lockfile
bun run dev
```

Open [http://localhost:3456](http://localhost:3456). On first run, maestro asks for the directory that contains your git repositories.

`bunfig.toml` sets a seven-day minimum release age for newly resolved dependency versions. Keep `bun.lock` committed when intentionally updating dependencies.

## Commands

```bash
bun run dev                    # start the dev server with file watching
bun run start                  # start the server without file watching
bunx --no-install tsc --noEmit  # type-check using the installed compiler
bun bin/claudesk.mjs --no-open # run the CLI entry without opening a browser
```

The CI workflow runs on branch pushes, pull requests, and merge queue checks. It uses Bun 1.3.14, installs from the frozen lockfile with lifecycle scripts disabled, and runs the TypeScript check above. Dependency review runs separately.

## Notes

- Requires Bun and an OpenCode setup with authenticated provider credentials.
- Configuration is stored in `~/.maestro/config.json`; legacy `~/.claudesk/config.json` is read if present.
- Set `CLAUDESK_PORT` or `PORT` to override the default port `3456`.
- Session JSON is persisted under repo-root `.maestro/sessions`; legacy `.claudesk/sessions` files can be imported.
- `repoBlacklistPatterns` in the config can hide repositories from the launch list.
- OpenCode file attachments are not supported yet.
- There is no build step, linter, or test command configured; TypeScript runs directly through Bun.

## Architecture

![maestro architecture diagram](./architecture.png)

## License

[MIT](LICENSE)

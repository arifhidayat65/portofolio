# AGENTS.md

## What this is

A **Vue 2** (2.6.11) single-page portfolio app built with `@vue/cli-service` 4.3.1 / webpack 4.47 and Bootstrap 4.5. The `Nextjs` folder name and README are misleading — there is **no Next.js/React here**. Do not treat it as such.

## Commands

- Dev server: `npm run serve` (README's `npm run dev` does not exist)
- Lint: `npm run lint` (`vue-cli-service lint`)
- Build: see gotchas below

## Gotchas (verified)

- **Node 22 + webpack 4 needs OpenSSL legacy provider.** webpack 4's md4 hashing is rejected by OpenSSL 3, so any build/dev command fails with `ERR_OSSL_EVP_UNSUPPORTED` unless `NODE_OPTIONS=--openssl-legacy-provider` is set. On Windows PowerShell: `$env:NODE_OPTIONS="--openssl-legacy-provider"; npx vue-cli-service serve` (or `... build`).
- **The `start` and `build` npm scripts are broken.** They prepend `export SET NODE_OPTIONS=...`, which is bash syntax and fails on Windows; even in bash it exports a variable named `SET`. Don't use them verbatim — set `NODE_OPTIONS` yourself and call `vue-cli-service` directly via `npx`.
- **`config.js` is currently invalid JS.** It has a stray AdSense `<script>` HTML tag pasted in (same paste bug exists in `.env`). `node --check` fails on it, and Contact.vue imports it, so builds will break until the HTML is removed. Watch for new `<script>`/AdSense cruft in any file.
- **`.env` is committed to git** (only `.env.*.local` are gitignored) and contains placeholder secrets. Don't add real secrets to it; don't commit credential changes.

## Where content lives

- **`info.js` (repo root) is the single source of truth** for all site content: name, links, education, experience, skills, portfolio items, and design portfolio. Components import it as `../../info`. To change content, edit `info.js` — not the Vue components.
- **`config.js` holds EmailJS credentials** (`serviceID`/`templateID`/`userID`) used by `Contact.vue` for the contact form.
- Images are required via `require("./src/assets/...")` inside `info.js` — new assets must go in `src/assets/`.

## Architecture notes

- `src/main.js` sets up Vue Router in `history` mode with a single `/` route; sections (`about`, `skills`, `portfolio`, `contact`) are reached by scrolling, not routing.
- `netlify.toml` only has an SPA redirect (`/*` → `/index.html`), which is required for history-mode routing on Netlify. No build command is set there.
- `vue.config.js` deletes the eslint webpack rule, so **ESLint never runs at build/dev time** — only via `npm run lint`.
- Components follow **Vue 2 Options API** (`data`/`methods`/`props`) and pass a `nightMode` prop; night mode persists via `vue-cookie`.
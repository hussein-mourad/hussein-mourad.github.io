# AGENTS.md

Personal portfolio for Hussein Mourad, published to GitHub Pages at
https://hussein-mourad.github.io/

## Branching model
This repo is an Astro-only portfolio site. The live branch is `main`.
Work on `main`; push to deploy.

## Deployment
GitHub Pages is set to "Deploy from a branch" on `main`. Pushing to `main`
auto-deploys. If deploying via GitHub Actions (e.g., Astro static output to
`dist/`), change Pages source to "GitHub Actions" and re-run
`.github/workflows/deploy.yml`.

The repo was renamed to lowercase (`hussein-mourad.github.io`); the git remote
is SSH: `git@github.com:hussein-mourad/hussein-mourad.github.io.git`.

## Git push auth gotcha
The `gh` OAuth token lacks the `workflow` scope, so pushing branches that
contain `.github/workflows/*` over HTTPS is rejected. The remote is set to SSH
for this reason. Keep it SSH; do NOT switch back to HTTPS unless
`gh auth refresh -h github.com -s workflow` has been run first.

## Dev commands
- `npm run dev` — starts dev server on localhost:4321
- `npm run build` — outputs to `dist/`
- `npm run preview` — preview production build

## Astro notes
- `astro@5`, static output to `dist/`, `base: "/"`.
- CI runs `npm ci`, so keep `package-lock.json` in sync: run `npm install`
  after changing deps. A `bun.lock` also exists (local `bun` use); if you add
  deps with bun, also regenerate `package-lock.json` or `npm ci` will fail.
- Styling: hand-written CSS in `src/styles/global.css` (Tailwind v4 planned —
  see `plan.md` before large changes).
- All content is data-driven from `src/data/site.ts` (when available) or
  component frontmatter.

## Don't commit
`node_modules/`, `dist/`, `.astro/`, `.DS_Store` are gitignored.

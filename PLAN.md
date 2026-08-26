# Astro Portfolio Redesign — Plan

## Goal

Redesign the `astro` branch into a polished, dark-themed portfolio (Tailwind) that
showcases projects (with images) and demonstrates skills, then make it the **live**
GitHub Pages site.

## Decisions

- **Stack:** Astro 5 + Tailwind CSS v4
- **Look & feel:** Minimal & elegant with subtle techy accents (monospace labels,
  faint grid/glow backdrop, availability badge)
- **Theme:** Dark only
- **Accent:** Teal (default) — single token, one-line change
- **Extras:** Project images + resume download (no blog, no testimonials)

## 1. Tech & dependencies

- Keep `astro@5`. Add: `tailwindcss` + `@tailwindcss/vite` (Tailwind v4, CSS-first
  `@theme` config, no JS config file).
- Self-hosted fonts via `@fontsource/inter` (sans) + `@fontsource/jetbrains-mono`
  (mono) — no external requests.
- Add `@astrojs/check` + `typescript` for type safety. Keep `@astrojs/sitemap` for SEO.
- Update `astro.config.mjs` to register the `tailwindcss()` Vite plugin.
- Replace `src/styles/global.css` with `@import "tailwindcss";` + `@theme` tokens
  (`--color-accent`, dark bg/surface/border palette) + base resets.

## 2. Content data layer (easy to edit)

Create `src/data/site.ts` (typed) holding all copy:

- `profile` (name, role, tagline, blurb, location, email, socials, available flag)
- `nav` links
- `about` paragraphs + small `stats` row
- `projects[]`: `{ title, description, tags[], image?, liveUrl, repoUrl, featured }`
- `skills[]` grouped: `{ category, items: { name, level }[] }`
- `experience[]`: `{ period, role, place, description }`
- `resume` path → `/resume.pdf`

Placeholder content stays; structure ready for real details.

## 3. Component redesign (Tailwind, dark-only, responsive, a11y)

- **Layout.astro** — HTML shell, SEO/OG meta, font imports, `<slot/>`, reduced-motion.
- **Header.astro** — sticky blurred nav, logo, mobile hamburger, active-section
  highlight (IntersectionObserver), social icons.
- **Hero.astro** — large name with gradient accent, mono role label, tagline, CTAs
  (View work + Download CV), subtle animated grid/glow backdrop, availability badge.
- **About.astro** — two-column text + stat cards.
- **Projects.astro + ProjectCard.astro** — responsive grid; cards with image
  thumbnail (CSS-gradient placeholder if no image), hover lift, tag chips,
  live/source links, featured badge.
- **Skills.astro** — grouped categories, animated proficiency bars (scroll-triggered).
- **Experience.astro** — vertical timeline with accent dots.
- **Contact.astro** — strong CTA, email + social icons.
- **Footer.astro** + **Reveal.astro** (scroll-reveal) + **Icons.astro** (inline SVGs).

## 4. Static assets

- `public/favicon.svg`, placeholder `public/resume.pdf` (replace with real CV).
- Project images: CSS gradient placeholders by default; real images in
  `public/projects/` auto-supported via the data field.

## 5. Make Astro the live site

Currently Pages serves `main` (Deploy from a branch). To go live with Astro:

1. Set Pages source to **GitHub Actions** via `gh api` (`build_type: workflow`).
2. Set default branch → `astro`.
3. Re-run `.github/workflows/deploy.yml` (push or workflow_dispatch) → publishes `dist/`.
   `jekyll` / `react-vite` / `main` branches remain as alternates (optional to prune later).

## 6. Verification

- `npm install`, `npm run build` (must succeed), `npm run dev` to eyeball.
- Push `astro` → confirm Actions workflow deploys → `https://hussein-mourad.github.io/`
  shows the new design.

## Out of scope

No blog, no testimonials. Real copy/images/PDF are placeholders to be filled via
`src/data/site.ts` + `public/`.

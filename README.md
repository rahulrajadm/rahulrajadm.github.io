# rahulrajadm.github.io

Personal portfolio site for Rahul Raja Durai Murugan — live at [rahulrajadm.github.io](https://rahulrajadm.github.io).

**Repo name decision:** this repo is named `rahulrajadm.github.io` on purpose — GitHub Pages treats a repo with this exact name as a *user site*, deployed at the domain root (`https://rahulrajadm.github.io`) with no base path. Every internal link and asset path in this project assumes the root, and `astro.config.mjs` has no `base` set. If this repo is ever renamed, every link breaks.

## Stack

[Astro](https://astro.build) — static output, no client-side framework. Chosen because this is a content site (projects, research, resume), not an app; a heavy SPA would hurt first paint, SEO, and link sharing.

## Local development

```bash
npm install
npm run dev
```

Requires Node (see `.nvmrc` for the pinned version).

## Build

```bash
npm run build
```

Outputs static files to `dist/`.

## Deploy

Deployment is automatic: every push to `main` triggers `.github/workflows/deploy.yml`, which builds the site with [`withastro/action`](https://github.com/withastro/action) and publishes the build artifact via `actions/deploy-pages`. GitHub Pages must be configured (Settings → Pages → Build and deployment → Source: **GitHub Actions**) — this is a one-time repo setting, not something the workflow itself can toggle.

`public/.nojekyll` is required so GitHub's default Jekyll processing doesn't strip Astro's `_astro/` asset directory (anything starting with `_`).

## Status

Early scaffold — placeholder content only. Real pages, design system, and content are being built out in stages; see project history for progress.

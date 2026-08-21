# hiretayler.com

Tayler Coon's portfolio. Static Astro site with hand-written CSS, deployed to GitHub Pages behind Cloudflare.

## Dev

```bash
npm install
npm run dev       # localhost:4321
npm run build     # outputs ./dist
npm run preview   # serves the built site
```

## Deploy

Pushes to `main` trigger `.github/workflows/deploy.yml`, which builds with Node 22 and publishes `./dist` to GitHub Pages. The `public/CNAME` file binds the deployment to `hiretayler.com` — configure DNS at your registrar:

| Type  | Host | Value                                                               |
| ----- | ---- | ------------------------------------------------------------------- |
| A     | @    | 185.199.108.153, 185.199.109.153, 185.199.110.153, 185.199.111.153 |
| CNAME | www  | tayler-made-code.github.io                                          |

In GitHub → Settings → Pages, set source to "GitHub Actions" and enable "Enforce HTTPS" after the cert provisions.

## Structure

- `src/pages/index.astro` — the whole site
- `src/components/` — navigation, project cards, project previews, inquiry dialog, and footer
- `src/layouts/Base.astro` — shared document shell and social metadata
- `src/styles/global.css` — design tokens and responsive page styles
- `public/` — deployable images, social/favicons, CNAME, and the static résumé

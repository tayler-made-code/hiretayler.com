# hiretayler.com

Tayler Coon's portfolio. Static site, Astro + Tailwind, deployed to GitHub Pages.

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
- `src/components/` — Prompt, Line, ProjectRow, Caret primitives
- `src/layouts/Base.astro` — shared shell (meta tags, font load)
- `src/styles/global.css` — Tailwind + theme tokens (`@theme` block)
- `public/` — static passthroughs (CNAME, resume.pdf, graybox.html, favicons)

# Voltworks Website

The official Voltworks marketing website — a React + Vite single-page app deployed to GitHub Pages on a custom domain.

---

## Quick Start

```bash
npm install      # install dependencies
npm run dev      # start local dev server at http://localhost:3000
npm run build    # build production bundle into dist/
npm run preview  # preview the production build locally
npm run deploy   # build + publish dist/ to the gh-pages branch
```

You need **Node.js 18+** installed.

---

## Tech Stack

- **React 19** + **TypeScript** — UI
- **Vite 6** — build tool / dev server
- **Tailwind CSS 4** — styling
- **React Router 7** — client-side routing
- **Framer Motion** — animations
- **Lucide React** — icons
- **@google/genai** — Gemini API integration (requires `GEMINI_API_KEY` in `.env`)

---

## Project Structure

```
.
├── index.html              # Vite entry HTML
├── vite.config.ts          # Vite config (base path lives here — see Deployment)
├── package.json
├── data/
│   ├── blog.json           # Blog post content
│   └── voltworks_products.json  # Product catalog
└── src/
    ├── main.tsx            # React entry point
    ├── App.tsx             # Root component + routes
    ├── index.css           # Global styles / Tailwind directives
    ├── pages/              # Top-level route pages (Home, Products, Career, etc.)
    ├── components/         # Reusable UI components
    ├── lib/                # Utilities, helpers, API clients
    └── public/             # Static assets served as-is
```

---

## Editing Content

- **Products** → edit `data/voltworks_products.json`
- **Blog posts** → edit `data/blog.json`
- **Page copy** → edit the matching file in `src/pages/`
- **Images / static files** → drop into `src/public/`

After editing, run `npm run dev` to preview, then `npm run deploy` to publish.

---

## Deployment

The site is deployed via the **gh-pages** package to the `gh-pages` branch of this repo, then served by GitHub Pages on the custom domain configured in **Settings → Pages**.

```bash
npm run deploy
```

This runs `npm run build` then pushes `dist/` to the `gh-pages` branch.

### Important: the `base` path in `vite.config.ts`

- **Custom domain** (current setup) → `base: '/'`
- **GitHub Pages default URL** (`username.github.io/PWeb/`) → `base: '/PWeb/'`

If you ever remove the custom domain, you must switch `base` back to `/PWeb/` or all assets will 404 and the page will render blank.

### Custom domain (CNAME)

The custom domain is stored as a `CNAME` file in the published `gh-pages` branch. GitHub Pages re-applies it from the repo Settings on each deploy. If the domain disappears after a deploy, re-set it under **Settings → Pages → Custom domain**.

DNS should point to GitHub Pages' IPs (apex) or `username.github.io` (CNAME record for `www`).

---

## Environment Variables

Create a `.env` file in the project root (not committed) with:

```
GEMINI_API_KEY=your_key_here
```

This is wired into the client via `vite.config.ts` and used by `@google/genai`.

---

## Troubleshooting

**Page is blank, console says stylesheet failed to load**
The `base` in `vite.config.ts` doesn't match how the site is served. See [Deployment](#deployment).

**Custom domain stopped working after a deploy**
Re-set the domain under Settings → Pages. The `CNAME` file in `gh-pages` may have been overwritten.

**`npm run dev` fails on a fresh clone**
Delete `node_modules` and `package-lock.json`, then `npm install` again.

---

## Contact

Owner: **voltworks.management@gmail.com**

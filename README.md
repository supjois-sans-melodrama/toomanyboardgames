# Too Many Board Games

A React dashboard analyzing 680 real BoardGameGeek titles — k-means
clustering, ridge regression, and PCA to answer "what actually predicts a
good board game." See the app itself (the "How This Works" tab) for full
methodology notes and dataset provenance.

## Project structure

```
toomanyboardgames/
├── index.html          # Vite entry HTML, loads Tailwind via CDN
├── package.json
├── vite.config.js
├── render.yaml          # Render Blueprint (see "Deploy" below)
├── .gitignore
└── src/
    ├── main.jsx          # Mounts <App /> into #root
    └── App.jsx           # The full dashboard component
```

## Run locally

```bash
npm install
npm run dev
```

Then open the URL Vite prints (usually http://localhost:5173).

## Build for production

```bash
npm run build
```

Outputs a static site to `dist/`. Preview it locally with `npm run preview`.

## Deploy to Render

**Option A — Blueprint (recommended):** push this repo to GitHub, then in
Render click **New → Blueprint** and point it at the repo. Render reads
`render.yaml` and configures the static site automatically — no manual
settings needed.

**Option B — Manual static site:** click **New → Static Site**, connect the
repo, and set:
- **Root Directory:** leave blank (repo root)
- **Build Command:** `npm run build`
- **Publish Directory:** `dist`

> If a build ever fails with `npm error ... no such file or directory, open
> '.../src/package.json'`, the Root Directory field has been set to `src` by
> mistake — clear it so Render looks in the repo root, where `package.json`
> actually lives.

## Notes

- Styling uses the Tailwind **Play CDN** (`<script src="https://cdn.tailwindcss.com">`
  in `index.html`) for zero-config setup. This is fine for this project's
  scale, but for a larger production app, switch to a real Tailwind build
  (`npm install -D tailwindcss @tailwindcss/vite`) so CSS isn't compiled in
  the visitor's browser on every page load.
- All data (the 680-game dataset, cluster/regression output, and the recent-
  games supplement) is bundled directly into `App.jsx` — no backend or API
  calls required.

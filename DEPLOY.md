# Deploy — Hôtel Lagune Balmer (Vercel + Astro static)

Static Astro site. Output: `dist/`. No server adapter required.

## Prerequisites

- Node.js `>= 22.12`
- GitHub repo (push when auth is ready)
- Vercel account

## Local check

```bash
cd hotel-lagune-balmer
npm install
npm run build   # must write to dist/
npm run preview # optional: http://localhost:4321
```

## Vercel (recommended)

1. Import the GitHub repo at [vercel.com/new](https://vercel.com/new).
2. Framework Preset: **Astro**
3. Build Command: `npm run build`
4. Output Directory: `dist`
5. Install Command: `npm install`
6. Deploy.

Or CLI (after `npx vercel login`):

```bash
npx vercel
```

Production promote:

```bash
npx vercel --prod
```

## Notes

- Pure static HTML/CSS/JS — no SSR, no env secrets required for the demo.
- WhatsApp CTAs are client-side `wa.me` links from `src/data/hotel.json`.
- Do not commit `node_modules/` or `dist/` (see `.gitignore`).

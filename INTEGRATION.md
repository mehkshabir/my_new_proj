# BUOYANCY° — project notes

## This is now a complete, standalone, deployable project
I don't have your actual existing repo — only the 3 reference images, the dither video,
and the geology-demo code from earlier in this chat. So this zip is a full working Vite
+ React + TypeScript + Tailwind project on its own: `npm install && npm run dev` works
right out of the box, and it's already been build-tested (`npm run build` succeeds clean).

It includes a **Home** page built from the cursor-reveal effect we made earlier
(rebranded, with your dither video as the hero background) plus the **About / Pricing /
Contact** pages, all sharing one design system.

**If you have a separate existing site** you want this merged into instead: copy
everything under `src/` into your project (matching paths), skip the root config files
(`package.json`, `vite.config.ts`, etc. — you already have your own), add
`react-router-dom` to your dependencies, and wire the routes into your existing router.
Swap `src/components/Nav.tsx` / `Footer.tsx` and the variables in `src/styles/theme.css`
for your real ones if they differ — nothing else is hard-coded, so the new pages will
pick up your real branding automatically.

## Files created
```
src/styles/theme.css          — design tokens (colors, fonts, animation keyframes) shared by new pages
src/components/Nav.tsx        — pill nav, reused across all 3 new pages
src/components/Footer.tsx     — footer, reused across all 3 new pages
src/components/DiveReadout.tsx— small "dive computer" stat chip (signature element)
src/pages/About.tsx           — About Us (hero: dive-cliff.jpg)
src/pages/Pricing.tsx         — Dives & Pricing (hero: gear-flatlay.jpg)
src/pages/Contact.tsx         — Contact Us (hero: diver-descent.jpg)
src/assets/dive-cliff.jpg     — from your uploaded reference image 1
src/assets/diver-descent.jpg  — from your uploaded reference image 2
src/assets/gear-flatlay.jpg   — from your uploaded reference image 3
src/assets/dither-hero.mp4    — your dither video, for optional use as a Home hero background
src/App.example.tsx           — reference only: shows how routes plug in, don't overwrite your App.tsx
```

## Files you need to touch in your real project
1. **`package.json`** — add `react-router-dom` if you don't already have routing:
   ```
   npm install react-router-dom lucide-react
   ```
2. **Your `App.tsx`** — add the three routes (see `App.example.tsx` for the pattern).
   If you're not using React Router yet, any routing setup (Next.js file-based routing,
   etc.) works the same way — just drop `About.tsx` / `Pricing.tsx` / `Contact.tsx`
   into the matching route files.
3. **`src/main.tsx` or your root entry** — import `src/styles/theme.css` once, globally
   (after your existing Tailwind `@tailwind` directives so the CSS variables are available).
4. **Nav links on your existing Home page** — point them at `/about`, `/pricing`,
   `/contact` so visitors can actually reach the new pages.

## Design choices, briefly
- **Palette**: near-black teal `#071410` background, bioluminescent cyan `#4be3c9` accent
  — pulled straight from the glow in your reference photos, rather than reusing the
  orange accent from the geology demo.
- **Signature element**: the "dive readout" chips (`DiveReadout.tsx`) echo the glowing
  dive-computer display in your gear photo — depth, temp, and visibility stats appear
  as HUD-style chips throughout instead of generic icon+text feature lists.
- **Imagery mapping**: cliff-wall diver → About (site storytelling), gear flatlay →
  Pricing (packages/equipment), descending diver → Contact (moodier, "start your journey"
  framing). Swap freely if you had different pages in mind for each.
- All copy (Churna Island details, pricing, contact info) is placeholder — replace with
  your real rates, certifications, and contact details before publishing.

## Run & deploy
```bash
npm install
npm run dev          # check http://localhost:5173/about, /pricing, /contact
npm run build         # production build
vercel                # deploy (or connect the repo in the Vercel dashboard for auto-deploys on push)
```

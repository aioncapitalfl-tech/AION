# AION Capital – Loan Intake App

Mobile-first loan intake web app for AION Capital. This guide shows the **fastest path to launch on Vercel**, plus optional upgrades.

---

## 1) Requirements
- Node 18+
- A Next.js/React project containing the canvas code (the page/component you have).
- Tailwind + shadcn/ui already wired (as in your canvas code).

> The app works out-of-the-box with a **mailto fallback** for submissions. For a serverless endpoint, add Formspree (see §4).

---

## 2) Quick Start (Local)
```bash
# install deps
npm install

# run dev
npm run dev

# build prod
npm run build
npm start
```

Make sure images referenced in the code exist (the canvas uses `/mnt/data/b.png` while editing here—replace it with your own image path in your project, e.g. `/public/bg.webp`).

---

## 3) Deploy to Vercel (Recommended)
1. Push your code to GitHub.
2. Go to https://vercel.com → **New Project** → **Import** your repo → **Deploy**.
3. (Optional) Add a custom domain: Project → **Settings → Domains**.

If you want to use this config file, place `vercel.json` at the repo root (already generated for you).

---

## 4) Enable Real Submissions (Formspree)
1. Create a Formspree project and copy your endpoint, e.g. `https://formspree.io/f/xxxxxx`.
2. In the code, set:
```ts
const SUBMIT_ENDPOINT = "https://formspree.io/f/xxxxxx";
```
3. Commit & push. Vercel redeploys automatically.

**Data sent** (JSON): loanKind, amountDesired (raw number), firstName, lastName, email, phone, businessName, monthlyRevenue (raw number), industry, creditScoreRange, useOfFunds, consent.

---

## 5) Optional – Add PWA (Installable)
- Create `public/manifest.webmanifest`:
```json
{
  "name": "AION Capital – Loan Intake",
  "short_name": "AION Apply",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#000000",
  "theme_color": "#39ff14",
  "icons": [
    { "src": "/icons/icon-192.png", "sizes": "192x192", "type": "image/png" },
    { "src": "/icons/icon-512.png", "sizes": "512x512", "type": "image/png" }
  ]
}
```
- In your root layout/head, add:
```html
<link rel="manifest" href="/manifest.webmanifest" />
<meta name="theme-color" content="#39ff14" />
```
- (Optional) Register a simple service worker for offline shell.

---

## 6) Optional – Privacy & Anti‑Spam
- Link the consent text to your Privacy/Terms pages.
- Add a honeypot field or reCAPTCHA if needed (Formspree/Basin support this).

---

## 7) Troubleshooting
- **Blank page after deploy** → Check image paths. Use `/public/...` assets.
- **Modules not found** → Ensure `@/components/ui/*` exists (shadcn/ui setup).
- **Forms not sending** → If no `SUBMIT_ENDPOINT`, app falls back to `mailto:` using the device’s default email client.

---

## 8) What to send to clients
- Public URL (e.g., `https://your-app.vercel.app`)
- A short message: “For best experience, use a modern mobile browser.”
- If you added PWA, suggest: “Add to Home Screen.”

---

**Support**: aioncapitalfl@gmail.com • 321-607-0070
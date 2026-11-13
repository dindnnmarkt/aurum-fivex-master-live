# AURUM FIVEX PRO — Royal Gold Elite V3

Premium visual redesign of Obsidian Gold V2. Keeps the original `app.js`, TradingView Chart widget, Dashboard, Signals, History, Settings, local preferences, and optional public signal API integration.

## Update existing Cloudflare Workers deployment

1. Back up the current GitHub repository.
2. Upload **all files from the ZIP root** to the `main` branch of `dindnnmarkt/aurum-fivex-master-live`, replacing matching files. `index.html` is the redesigned UI. `app.js` and `sw.js` are preserved from V2. `wrangler.jsonc` configures static assets.
3. If your existing repository contains additional production configuration, compare before overwriting.
4. Check Cloudflare Workers & Pages > Deployments for Ready.
5. Open the workers.dev URL, hard refresh, and test all five tabs. On iPhone, close and reopen the installed Home Screen app. Service worker caches can require reload.

## What is real and what is not

- TradingView Chart is a real embedded external widget (internet required).
- Dashboard illustration, sample market price, signals, history and performance are DEMO until a compatible backend API is configured.
- This redesign does not enable live webhook, real iOS push, authentication, or order execution.
- Never put webhook secrets into client-side Settings.


V4: Official supplied logo in header and PWA icons; branding AURUM FIVEX PRO. Keep existing Cloudflare deployment and wrangler.jsonc.

# AURUM FIVEX MASTER — Obsidian Gold Luxury PWA

A working static PWA frontend with Dashboard, Signals, History and Settings. **All bundled trade values are fictional demo data.** No trading orders are placed.

## iPhone deployment (no PC required)

1. Create/open your GitHub repository on iPhone Safari.
2. Upload `index.html`, `app.js`, `sw.js`, `manifest.webmanifest`, `icon.svg` to the **repository root** (not a nested folder).
3. Deploy the repository to Cloudflare Pages, using framework preset `None`, build command blank, and output directory `/` (root). Alternatively use GitHub Pages with HTTPS.
4. Open the deployed HTTPS link in iPhone Safari → Share → Add to Home Screen → Add.
5. Navigate all four tabs. Demo works without backend. Settings are saved in this browser using localStorage.

Note: Opening `index.html` from the iPhone Files app is **not** equivalent to hosting a PWA. Service workers and Add to Home Screen require HTTPS hosting (or localhost during development).

## LIVE signal integration

The frontend expects `GET https://YOUR-WORKER.workers.dev/api/signals` returning:

```json
{"signals":[{"id":"evt-001","side":"BUY","entry":4010.2,"sl":3998.2,"tp":[4014.4,4018.6,4024.6,4030.6,4037.2],"mode":"FAST+","time":"2026-11-13T09:35:00+08:00","timeframe":"M5","result":"OPEN","pips":null,"extra":[4046.2,4058.2,4070.2]}]}
```

The optional Cloudflare Worker example in `backend/worker.js` receives TradingView webhook alerts at `POST /webhook` and stores up to 100 signals in Cloudflare KV. This is an **integration template**, not a deployed service. It requires a KV namespace binding `SIGNALS_KV` and secret `WEBHOOK_SECRET`. Set the worker `ALLOWED_ORIGIN` environment variable to the **exact** HTTPS PWA origin for CORS. In Settings, enter the Worker base URL (without `/api/signals`). The app polls every 15 seconds while open. Background push notifications are **not implemented**.

Do not put the webhook secret into frontend JavaScript, GitHub public source or the app Settings. Keep webhook URL private: TradingView webhooks do not support custom auth headers; the example accepts a secret in the JSON body. To prevent public signal access, add server-side authentication before sharing publicly or selling subscriptions. This sample read endpoint is PUBLIC and should only be used for non-confidential signals.

## Alert JSON in TradingView

```json
{"secret":"YOUR_SECRET","id":"{{ticker}}-{{time}}-BUY","side":"BUY","entry":{{close}},"sl":3998.20,"tp":[4014.40,4018.60,4024.60,4030.60,4037.20],"mode":"FAST+","time":"{{timenow}}","timeframe":"{{interval}}"}
```

This is a **sample BUY payload only**. Replace fixed SL/TP with values calculated by your Pine indicator via `alert()` and send SELL with the correct direction. `{{close}}` is the chart price at alert firing; it may differ from the actual indicator entry. Prefer sending the indicator's own entry price. Never place credentials in Pine code intended for distribution.

## Limitations

- No live market-price feed or real candlestick feed; chart and Dashboard quote are demo placeholders even when API signals are enabled.
- No real account login, subscription billing, broker trading or push service.
- No claim that historical results or demo pips represent actual trading performance.
- Worker KV is eventually consistent and not an ideal transactional store; use a database with auth for production/customer deployment.
- The included icon is a new generic crown monogram, **not** the user's original brand logo.


## TradingView Chart (V2)
- Added **Chart** tab with TradingView Advanced Chart widget, `OANDA:XAUUSD`, M5/M15/H1/H4.
- Widget loads only when Chart is opened and requires internet.
- The widget is independent of the webhook and cannot display private Pine Script indicators.
- After deploying HTTPS, open Chart to verify TradingView can load on your iPhone.
- The dashboard illustration and sample price remain DEMO until a separate market-data integration is implemented.

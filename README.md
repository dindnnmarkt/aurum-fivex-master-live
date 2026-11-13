# AURUM FIVEX PRO — Royal Gold Elite FINAL V5

## Isi pakej
- `index.html`, `app.js`, `sw.js`, `manifest.webmanifest`: PWA dengan Dashboard, Chart, Signals, History, Settings.
- `aurum-fivex-logo-original.png`: **logo asal yang dibekalkan**, tanpa reka semula.
- `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`: ikon aplikasi daripada logo asal.
- `wrangler.jsonc`: Cloudflare Workers Static Assets; **nama Worker lama dikekalkan** supaya URL tidak berubah.
- `backend/worker.js`: contoh backend berasingan, **bukan** webhook aktif.

## Kemas kini GitHub dan Cloudflare
1. Buat backup repository GitHub sedia ada.
2. Upload **kandungan di dalam ZIP**, bukan ZIP itu sendiri, ke root repository GitHub `dindnnmarkt/aurum-fivex-master-live` pada branch `main`.
3. Gantikan fail bernama sama. Pastikan `index.html`, `app.js`, `sw.js`, `wrangler.jsonc` berada di root. Fail lama yang tidak ditindih boleh kekal, tetapi tidak digunakan.
4. Commit, kemudian semak status **Ready** untuk commit terbaru dalam Cloudflare Workers.
5. Uji `https://aurum-fivex-master-live.dindnnmarkt.workers.dev/?app=v5`. Jika paparan lama masih keluar, buka Incognito dan semak commit Cloudflare, kemudian clear site data/service worker bagi laman itu.
6. Untuk iPhone: Safari > Share > Add to Home Screen selepas versi baru disahkan.

## Semakan fungsi
- Dashboard: demo harga/candlestick dan pilihan mode.
- Chart: TradingView Advanced Chart widget `OANDA:XAUUSD`, pilihan M5/M15/H1/H4. Memerlukan internet dan servis TradingView.
- Signals: rekod demo dengan entry, SL, TP1–TP5.
- History: penapis ALL/BUY/SELL.
- Settings: tetapan disimpan dalam localStorage; API URL pilihan untuk backend yang serasi.

## Had penting
Carta TradingView adalah widget pasaran sebenar, **bukan** indikator Pine Script peribadi. Harga Dashboard, statistik, signal dan history masih **DEMO** sehingga API backend yang sebenar dihubungkan. Webhook, push notification sebenar, login dan trading automatik belum aktif. Jangan letak token rahsia dalam kod frontend.

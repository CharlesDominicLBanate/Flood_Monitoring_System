# Flood EWS — installable app (PWA)

This folder turns the Streamlit dashboard into an installable app (home screen on
Android/iOS, desktop app in Chrome/Edge). It is a thin shell: `index.html` embeds your
deployed Streamlit app, and `sw.js` caches the shell so it opens instantly.

## Files
- `index.html` – app shell (loading, offline and retry screens, embeds the dashboard)
- `manifest.json` – name, colors, icons
- `sw.js` – service worker (caches the shell files)
- `icons/` – app icons (192/512, maskable 192/512, Apple touch icon)

## Setup
1. Deploy the Streamlit app (e.g. Streamlit Community Cloud).
2. Edit `index.html` and set `APP_URL` to the deployed address (keep `?embed=true`).
3. Host this `pwa/` folder over **HTTPS** (GitHub Pages, Netlify, Cloudflare Pages).
   Service workers and installation do not work from `file://` or plain HTTP
   (except `http://localhost` for testing).
4. Open the page, then use **Install app** (Chrome/Edge) or **Share → Add to Home Screen** (iOS).

## Test locally
```bash
cd pwa
python -m http.server 8000
# open http://localhost:8000
```

## Notes
- The dashboard itself still needs internet (live weather). Offline, the app shows a retry screen.
- After editing any shell file, bump `CACHE_NAME` in `sw.js` (e.g. `flood-ews-shell-v2`) so
  installed copies update.
- Icons are not cached in the service worker beyond 192/512; that is intentional.

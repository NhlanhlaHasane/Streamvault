# StreamVault — Live IPTV Web App

Watch thousands of free live TV channels in your browser.
Powered by [iptv-org/iptv](https://github.com/iptv-org/iptv).

---

## Project Structure

```
streamvault/
├── frontend/                 ← React app (deploys to Netlify)
│   ├── src/
│   │   ├── main.jsx          ← React entry point
│   │   └── App.jsx           ← Full application (all-in-one)
│   ├── public/
│   │   ├── manifest.json     ← PWA manifest
│   │   ├── sw.js             ← Service Worker
│   │   └── favicon.svg
│   ├── index.html
│   ├── vite.config.js
│   └── package.json
├── backend/                  ← Node.js API (optional, full-stack only)
│   ├── server/index.js       ← Express server + cron jobs
│   ├── server/utils/playlist.js
│   ├── schema.sql            ← PostgreSQL schema
│   └── package.json
├── docker/                   ← Full-stack Docker deployment
│   ├── docker-compose.yml
│   └── nginx/conf.d/streamvault.conf
├── netlify.toml              ← Netlify build config (auto-detected)
├── .env.example
└── .gitignore
```

---

## Push to GitHub

```bash
# 1. Create a new EMPTY repo on github.com (no README, no .gitignore)

# 2. Run these commands inside the streamvault folder:
git init
git add .
git commit -m "Initial commit — StreamVault IPTV app"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/streamvault.git
git push -u origin main
```

---

## Deploy to Netlify (no backend needed)

### Option A — Netlify UI (recommended)

1. Go to https://app.netlify.com → **Add new site** → **Import an existing project**
2. Choose **GitHub** and select your `streamvault` repo
3. Netlify reads `netlify.toml` automatically — settings are pre-filled:
   - Base directory: `frontend`
   - Build command: `npm install && npm run build`
   - Publish directory: `dist`
4. Click **Deploy site**
5. Live at `https://your-site-name.netlify.app` in ~60 seconds

**Custom domain:** Site settings → Domain management → Add custom domain

Every `git push` to `main` triggers an automatic redeploy.

### Option B — Netlify CLI

```bash
npm install -g netlify-cli
netlify login
cd streamvault
netlify deploy --prod
```

---

## Run Locally

```bash
cd frontend
npm install
npm run dev
# http://localhost:5173
```

---

## Full Stack (optional — adds user accounts, server-side health checks)

```bash
cp .env.example .env   # set PG_PASSWORD and JWT_SECRET
cd docker
docker-compose up -d
# Frontend: http://localhost:3000  |  API: http://localhost:4000
```

---

## Features

- 3,000+ free live TV channels worldwide
- HLS.js player with live/offline status indicators
- Search + filter by country, language, category
- Favorites + recently watched (localStorage)
- Dark / light mode
- Responsive — mobile, tablet, desktop
- Fullscreen + Picture-in-Picture
- Admin dashboard with stream statistics
- PWA — installable on Android/iOS

---

## License

MIT. Streams sourced from iptv-org/iptv.

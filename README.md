<div align="center">

# Stremio Addon Manager

[![Vue](https://img.shields.io/badge/Vue-3-4FC08D?logo=vuedotjs&logoColor=fff&labelColor=333&style=flat)](https://vuejs.org/)
[![Vite](https://img.shields.io/badge/Vite-5-646CFF?logo=vite&logoColor=fff&labelColor=333&style=flat)](https://vitejs.dev/)
[![Vercel](https://img.shields.io/badge/Vercel-deployed-000?logo=vercel&logoColor=fff&labelColor=333&style=flat)](https://stremio-addon-manager-delta.vercel.app)

[![Stremio](https://img.shields.io/badge/Stremio-API-8A5AAB?logo=stremio&logoColor=fff&labelColor=333&style=flat)](https://www.stremio.com/)

[![Stars](https://img.shields.io/github/stars/goddivor-stremio-addons/stremio-addon-manager?logo=github&logoColor=fff&label=Stars&labelColor=333&color=E3B341&style=flat)](https://github.com/goddivor-stremio-addons/stremio-addon-manager/stargazers)
[![Forks](https://img.shields.io/github/forks/goddivor-stremio-addons/stremio-addon-manager?logo=github&logoColor=fff&label=Forks&labelColor=333&color=8957E5&style=flat)](https://github.com/goddivor-stremio-addons/stremio-addon-manager/network/members)
[![Watchers](https://img.shields.io/github/watchers/goddivor-stremio-addons/stremio-addon-manager?logo=github&logoColor=fff&label=Watchers&labelColor=333&color=1F6FEB&style=flat)](https://github.com/goddivor-stremio-addons/stremio-addon-manager/watchers)
[![Contributors](https://img.shields.io/github/contributors/goddivor-stremio-addons/stremio-addon-manager?logo=github&logoColor=fff&label=Contributors&labelColor=333&color=DB61A2&style=flat)](https://github.com/goddivor-stremio-addons/stremio-addon-manager/graphs/contributors)
[![Open issues](https://img.shields.io/github/issues/goddivor-stremio-addons/stremio-addon-manager?logo=github&logoColor=fff&label=Issues&labelColor=333&color=3FB950&style=flat)](https://github.com/goddivor-stremio-addons/stremio-addon-manager/issues)

Reorder and prune your **Stremio** add-ons from a simple drag-and-drop page,
then push the new order back to your account — so a favourite source keeps its
rank instead of dropping to the bottom every time you re-add it. This is a
**self-hosted, hardened fork**: every network call goes only to the official
Stremio API, and the upstream analytics beacon has been removed.

</div>

## 🎖️ Features

- **Drag-and-drop reordering** — set the priority of every installed add-on (Cinemeta included) and sync it back to your account.
- **Remove add-ons** — drop any non-protected add-on from your collection.
- **Two sign-in methods** — log in with your Stremio email and password, or paste an `authKey`.
- **Credentials stay in memory** — nothing is written to local storage or cookies; it is gone the moment you refresh.
- **No telemetry** — the upstream `@vercel/analytics` page-view beacon was stripped out in this fork.

## 📋 Requirements

- A **Stremio account** (Facebook login is not supported).
- **Node.js 18+** — only if you build or run it locally; the hosted version needs nothing but a browser.

## 📦 Installation

Just want to use it? Open the hosted build: **https://stremio-addon-manager-delta.vercel.app**

To run your own copy:

```bash
git clone https://github.com/goddivor-stremio-addons/stremio-addon-manager.git
cd stremio-addon-manager
npm install
```

Or with Docker:

```bash
docker build -t stremio-addon-manager .
docker run -p 8080:80 stremio-addon-manager
# → http://localhost:8080
```

## ⚙️ Usage

> ⚠️ There is no undo. Note your current add-on order before your first sync — a bad sync can leave your collection in an unexpected state.

### 🧩 Reorder your add-ons

1. Open the app and authenticate (email + password, or an `authKey`).
2. Click **Load Addons** to pull your current collection.
3. Drag the add-ons into the order you want.
4. Click **Sync To Stremio** to write the new order back to your account.

### 🔑 Get your authKey manually

```js
// Log in to https://web.stremio.com/, open the browser console, and run:
JSON.parse(localStorage.getItem("profile")).auth.key
```

Paste the returned value into the app's auth-key field.

### 💻 Run locally

```bash
npm run dev      # dev server with hot reload
npm run build    # production build into dist/
npm run preview  # serve the production build locally
```

## 🤝 Contributing

Issues and pull requests are welcome on this fork. It tracks
[`pancake3000/stremio-addon-manager`](https://github.com/pancake3000/stremio-addon-manager)
as upstream; please keep commits in the conventional format.

## 📜 License

No license is declared upstream, and this fork adds none — no usage rights are
granted beyond those the original project already provides.

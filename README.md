# Falconry Log

A progressive web app (PWA) for falconers to track hawk weight, food intake, temperature, performance, and session notes. Built to be installed on Android as a home screen app and used hands-free in the field via voice commands.

**Live app:** https://windnfeathers.github.io/falconry_log/

---

## Features

- **Multiple bird profiles** — track any number of birds, each with species, band number history, arrival weight, and optional target weight range
- **Voice logging** — hands-free data entry; open the app, set the phone down, and speak
- **Independent entries** — each data point is its own timestamped record; no fields are assumed null means null
- **Manual entry with date/time picker** — backfill missed days or log multiple sessions per day
- **Edit and delete** — tap any history entry to correct it
- **Graphs** — weight over time (lowest per day), weight vs temperature, weight vs performance, food intake over time
- **Pre/post weight calculator** — enter pre-feed and post-feed weights to calculate food eaten; auto-saved to the entry
- **Journal** — free-text notes per entry via voice or manual input
- **Offline support** — works without internet once installed
- **Google Drive backup** — automatic backup after every save (requires OAuth setup below)
- **Export/import** — JSON backup and restore at any time
- **Units** — ounces, grams, or lbs + ounces

---

## Installation on Android

1. Open Chrome and go to https://windnfeathers.github.io/falconry_log/
2. Tap the three-dot menu
3. Tap **Install app**
4. The app will appear on your home screen and run in standalone mode

---

## Voice Commands

Once a bird is selected the app starts listening automatically (if enabled in Settings).

| Say | Does |
|---|---|
| "Weight" | Logs pre-feed weight |
| "Post-feed" | Logs post-feed weight and calculates food eaten |
| "Food" | Logs food type and weight (5 second window to give both) |
| "Temperature" | Logs outside temperature |
| "Performance" | Logs a 1–10 session rating |
| "Note" | Adds a journal entry |
| "Cancel" | Removes the last field entered without losing the rest |
| "Done" | Saves the entry and stops listening |

---

## Google Drive Backup Setup

Backup requires a free Google Cloud OAuth 2.0 client ID. This is a one-time setup.

1. Go to [console.cloud.google.com](https://console.cloud.google.com)
2. Create a new project (name it anything)
3. Go to **APIs & Services** > **Library** > search for **Google Drive API** > Enable it
4. Go to **APIs & Services** > **Credentials** > **Create Credentials** > **OAuth 2.0 Client ID**
5. Set application type to **Web application**
6. Under **Authorized JavaScript origins** add: `https://windnfeathers.github.io`
7. Under **Authorized redirect URIs** add: `https://windnfeathers.github.io/falconry_log/`
8. Copy the **Client ID**
9. In the app go to **Settings** > **Google Drive backup** > paste the Client ID > tap **Sign in with Google**

Once signed in, every save automatically backs up to your Google Drive app data folder. The backup file is not visible in your regular Drive — it lives in a hidden app-specific space only this app can access.

---

## App Icons

The manifest references `icon-192.png` and `icon-512.png`.

---

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire app — HTML, CSS, and JavaScript |
| `manifest.json` | PWA manifest for home screen installation |
| `sw.js` | Service worker for offline support and caching |
| `icon-192.png` | Home screen icon (192x192) |
| `icon-512.png` | Home screen icon (512x512) |

---

## Data Storage

All data is stored in your browser's `localStorage` on your device. No data is sent anywhere except to your own Google Drive if you enable backup. Clearing your browser site data will erase local data — use Export or Google Drive backup to protect it.

---

## Built With

- Vanilla HTML, CSS, JavaScript — no frameworks
- [Chart.js](https://www.chartjs.org/) for graphs
- Web Speech API for voice input and spoken confirmations
- Google Drive REST API for backup
- GitHub Pages for hosting

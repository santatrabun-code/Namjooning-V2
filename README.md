# 🚲 Namjooning — Daily Intentional Living Journal

> *"To me, the world is a big museum. We're all just looking for the pieces that speak to us."*

A personal PWA (Progressive Web App) built for daily journaling, mindful habits, and intentional living — inspired by the way RM (Kim Namjoon) of BTS moves through the world: reading, discovering music, visiting galleries, strolling, and reflecting.

---

## 📁 File Structure

```
namjooning-pwa/
├── index.html               ← The entire app (single file)
├── manifest.json            ← PWA configuration
├── sw.js                    ← Service worker (offline support)
└── icons/
    ├── icon-192.png         ← Home screen icon (Android / Chrome)
    ├── icon-512.png         ← Splash screen icon
    ├── apple-touch-icon.png ← Home screen icon (iOS / Safari)
    └── favicon-32.png       ← Browser tab icon
```

---

## ✨ Features

### Core Disciplines
| Feature | Description |
|---|---|
| 📖 **Reading Timer** | 15-minute countdown timer. When it completes, a field appears to log your book title and chapter. |
| 🎵 **Music Discovery** | Log an artist and song you discovered or listened to intentionally today. |
| 📓 **Bullet Journal** | A full-screen lined paper journal for daily reflection. Opens in a modal with a distraction-free writing experience. |

### Intentional Living Activities
Toggle activities you did today. Each one reveals a notes field for details.

- 🏛️ Museum
- 🌿 Stroll
- ⛰️ Hiking
- 🎨 Gallery
- ✨ Artistry Activity

### Archive & Search
- Monthly calendar grid showing completed days (🟡 highlighted = both reading and journaling done)
- Tap any day to view that day's log in read-only mode
- Keyword search filters and highlights matching days across your history

### Streak Counter
Tracks consecutive days where you completed both a reading session and a journal entry (more than 5 characters).

### Backup & Restore
- 💾 **Export** — Downloads a `.json` backup of all your data, timestamped
- 📂 **Import** — Restores from a previous backup, merging with existing data (imported days take precedence)

### Daily Quote
A rotating quote appears at the top each day, cycling through a curated bank of 50 reflections.

---

## 📲 Installation (PWA)

### Android / Chrome
1. Open the app URL in Chrome
2. An **"Install"** banner will appear at the top — tap it
3. Or tap the browser menu (⋮) → **"Add to Home Screen"**
4. The app installs like a native app with no browser chrome

### iOS / Safari
1. Open the app URL in Safari
2. Tap the **Share** button (□↑)
3. Scroll down and tap **"Add to Home Screen"**
4. Tap **Add**

### Desktop (Chrome / Edge)
1. Look for the install icon (➕) in the address bar
2. Click it and confirm

Once installed, the app works fully **offline** — no internet connection needed.

---

## 🚀 Deployment

The app is a static site — no server, no database, no build step. Host it anywhere that serves HTTPS.

### Option 1 — Netlify (Easiest, free)
1. Go to [netlify.com/drop](https://netlify.com/drop)
2. Drag and drop the `namjooning-pwa/` folder onto the page
3. Done — you get a live HTTPS URL instantly

### Option 2 — GitHub Pages (Free)
```bash
# 1. Create a new GitHub repository
# 2. Push the folder contents (not the folder itself)
git init
git add .
git commit -m "Initial deploy"
git remote add origin https://github.com/YOUR_USERNAME/namjooning.git
git push -u origin main

# 3. In repo Settings → Pages → Source: Deploy from branch → main → / (root)
```
Your app will be live at `https://YOUR_USERNAME.github.io/namjooning`

### Option 3 — Vercel (Free)
```bash
npm install -g vercel
cd namjooning-pwa
vercel deploy
```

> ⚠️ **HTTPS is required** for the PWA install prompt and service worker to activate. All three options above provide HTTPS automatically.

---

## 💾 Data & Privacy

All data is stored **locally on your device** using `localStorage`. Nothing is sent to any server. Your journal entries never leave your device.

- **Storage key:** `namjooning_v11`
- **Auto-migrates** data from `namjooning_v10` if present
- **Export regularly** using the 💾 button to back up your data — clearing your browser cache will erase it

---

## 🔧 Customisation

### Adding More Quotes
Open `index.html` and find the `QUOTES` array near the top of the `<script>` section. Add entries following the same pattern:

```javascript
{d: 51, q: "Your quote here."},
```

The `d` value is the day-of-year (1–365). If the day doesn't have an exact match, the app cycles through the bank automatically.

### Changing the Timer Duration
Find `let timeLeft = 900;` in the script and change `900` to any number of seconds:

```javascript
let timeLeft = 1800; // 30 minutes
```

### Adding New Activities
In the HTML, duplicate an `.act-container` block and give it a new ID. Then add the new activity name to the `ACTS` array in the script:

```javascript
const ACTS = ['museum','stroll','hiking','gallery','artistry','writing'];
```

---

## 🛠️ Technical Notes

- **No dependencies** — pure HTML, CSS, and vanilla JavaScript
- **No build step** — edit and deploy directly
- **Offline-first** — service worker caches all assets on first load
- **Safe-area aware** — padding accounts for notched phones (iPhone X+)
- **Streak logic** is capped at 366 iterations to prevent infinite loops
- **Archive safety** — the journal textarea is read-only when viewing past dates, preventing accidental overwrites of today's entry
- **Font:** DM Mono (monospace) + Playfair Display (serif for quotes/headings)

---

## 📋 Streak Conditions

A day counts toward your streak if it has:
1. A **reading entry** (book title field filled in, i.e. timer was completed)
2. A **journal entry** longer than 5 characters

Today is skipped (not penalised) if incomplete — the streak looks at yesterday and earlier.

---

*Built with 💛 for slow, intentional days.*

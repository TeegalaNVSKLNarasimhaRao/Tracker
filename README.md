# My Schedule & Habit Tracker

A personal daily planner, habit tracker, diary, and water logger — single HTML file, cloud-synced across all devices via Firebase.

**Live app:** [teegalanvsklnarasimharao.github.io/Tracker](https://teegalanvsklnarasimharao.github.io/Tracker/)

---

## What it does

- **Google Sign-In** — secure login, data tied to your Google account, works across every device automatically
- **Multiple user support** — each Google account gets a completely independent private data space
- **Real-time cloud sync** — changes on one device appear on all others within seconds
- **Offline support** — works without internet after first load, syncs when reconnected
- **Daily schedule** — separate tabs for Mon/Tue/Wed/Thu/Fri/Weekend, fully editable, mobile-friendly edit buttons
- **Habit tracker** — UUID-based habit keys mean reordering or deleting habits never corrupts historical data
- **Manage habits** — add, edit, delete, reorder, pause habits for date ranges
- **Heatmap** — 6-month visual consistency calendar
- **Diary** — daily journal with mood tags, auto-save every 30 seconds, Ctrl+S support
- **All Notes** — search, filter by mood, jump to any date
- **Water tracker** — 10-glass tracking, auto-ticks water habit at 2500ml, 7-day bar chart with ml labels
- **Holidays manager** — single day or date range, Indian holiday presets, auto schedule detection
- **Pomodoro timer** — timestamp-based (stays accurate in background), 25-min countdown on learning blocks
- **Daily snapshot** — one-tap text summary copyable to clipboard
- **Dark / Light mode toggle** — button shows current state, preference synced to cloud
- **Export / Import** — full JSON backup, safe merge on import, object URL cleanup
- **Auto data pruning** — water and focus data older than 60 days cleaned automatically

---

## How to access

Open the live URL from any browser on any device:

```
https://teegalanvsklnarasimharao.github.io/Tracker/
```

Sign in with your Google account. Your data loads from Firebase automatically.

**Add to home screen:**
- **Android (Chrome):** Three-dot menu → Add to Home Screen
- **iPhone (Safari):** Share → Add to Home Screen

---

## Data and privacy

| Item | Detail |
|------|--------|
| Storage | Firebase Firestore (Google cloud) |
| Auth | Google Sign-In via Firebase Authentication |
| Data isolation | Each user's data stored at `users/{uid}/data/` — no cross-user access |
| Security | Firestore rules: only authenticated owner can read/write own data |
| Offline | Firebase IndexedDB persistence — works without internet |
| Backup | Export button downloads full JSON backup |
| Pruning | Water + focus data auto-pruned after 60 days |
| Cost | Free tier — ~500KB/year, limit is 1GB |

---

## Features in detail

### Habit tracking — UUID-based keys
Every habit has a unique ID (e.g. `h001`, `hmo2x4k9j`). Tracker data is stored as `2026-04-20_h001` not `2026-04-20_h3`. This means:
- Reordering habits: historical data stays correct
- Deleting a habit: other habits' history is unaffected
- Renaming a habit: all past data still links correctly

### Diary
- Auto-saves after 30 seconds of inactivity
- Auto-saves when switching tabs or navigating dates
- Ctrl+S / Cmd+S for instant save
- Shows last entry date hint when today is empty
- Editable from both Diary tab and All Notes tab

### Schedule
- Edit/delete/reorder buttons always visible on mobile
- Pomodoro timer is timestamp-based — accurate even when screen sleeps
- Block colours have full dark mode overrides for proper contrast

### Water tracker
- Tapping any glass below goal removes the water habit tick (not just Reset button)
- Bar chart shows exact ml/L above each bar
- Streak counts consecutive days hitting 2500ml goal

### Sign-out safety
Sign-out correctly cleans up:
- Clears pending save debounce timer (prevents null crash)
- Clears diary auto-save timer (prevents saving empty data)
- Stops Pomodoro interval
- Removes Ctrl+S keyboard listener
- Resets session state (weekOff, moodFilter, currentMood) for next user

---

## Default habits

| # | Habit | Goal |
|---|-------|------|
| 1 | No phone on waking | First 30 min screen-free |
| 2 | Morning walk | At least 20 min |
| 3 | Big Data / DE course | Weekdays 9:30 / Weekends 10:30 |
| 4 | Finance study | Min 30 min |
| 5 | 2.5 L water | Track through the day |
| 6 | 20-20-20 eye rule | Every 20 min at screen |
| 7 | No Instagram before 7 PM | Keep the rule |
| 8 | Evening walk | At least 30 min |
| 9 | Screen-free dinner | No phone at table |
| 10 | Wind-down routine | Prayer / reflection before sleep |
| 11 | Asleep by 10:30 PM | Protect sleep window |

All habits can be added, edited, deleted, reordered, or paused in the Manage Habits tab.

---

## Default schedule highlights

**Weekdays (Mon/Tue/Fri):**
6:15 AM wake → walk → breakfast → personal time → 9:30 Big Data course (2hrs) → work calls → deep work → finance study → evening walk → dinner → scrum → wind down → 10:30 PM sleep

**Monday extra:** 9–10 PM call &nbsp;|&nbsp; **Wednesday extra:** 9:30–10 PM call &nbsp;|&nbsp; **Thursday extra:** 9–10 PM call

**Weekend:** Later start, prayer, longer walk, 1.5hr course, finance study, family time, weekly review, faith wind-down

---

## Firebase setup (already configured)

The app is connected to Firebase project `habbit-tracker-ef59d`. Required Firestore security rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/data/{docId} {
      allow read, write: if
        request.auth != null &&
        request.auth.uid == userId &&
        docId in ['meta', 'tracker', 'diary'];
    }
  }
}
```

Authorised domains must include `teegalanvsklnarasimharao.github.io` in Firebase → Authentication → Settings → Authorised domains.

---

## Files in this repository

| File | Description |
|------|-------------|
| `index.html` | The complete app — v10, production ready |
| `README.md` | This file |

---

## How to update

When a new version is available:
1. Export your data backup first (top bar → Export)
2. Replace `index.html` in this repository with the new version
3. GitHub Pages rebuilds within 1–2 minutes
4. Your cloud data is unaffected — it lives in Firebase, not in the file

---

## Tech stack

Pure HTML, CSS, and vanilla JavaScript in a single file. No frameworks. No build step. No dependencies except Firebase SDK loaded from CDN.

- **Firebase SDK:** v10.12.0
- **Auth:** Google OAuth via Firebase Authentication
- **Database:** Firebase Firestore (3 documents per user: meta, tracker, diary)
- **Offline:** `initializeFirestore` with `persistentLocalCache`
- **Storage key:** `tracker_dark` in localStorage (dark mode preference only)

---

*Personal productivity tracker. Tracking habits, learning, finance, and daily life from April 20, 2026.*

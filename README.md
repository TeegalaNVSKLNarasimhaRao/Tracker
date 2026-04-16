# My Schedule & Habit Tracker

A personal daily planner, habit tracker, diary, and water logger — all in a single HTML file. No installation. No account. No internet required after download.

**Live app:** [your-username.github.io/tracker](https://teegalanvsklnarasimharao.github.io/Tracker/)

---

## What it does

- **Daily schedule** — separate tabs for Monday, Tuesday, Wednesday, Thursday, Friday, and Weekend/Holiday. Each day is fully editable. Time blocks are colour-coded by type.
- **Habit tracker** — track up to any number of habits per day. Tap to mark done, skip, or leave empty. See weekly progress bars, monthly completion %, and a perfect-day streak counter.
- **Manage habits** — dedicated tab to add, edit, delete, and reorder habits. Pause any habit for a date range (e.g. during travel) so it does not affect your streak.
- **Heatmap** — 6-month visual calendar showing habit consistency. Darker = more habits done.
- **Diary** — one entry per day with mood tags (Great / Good / Okay / Low / Tough). Searchable across all entries.
- **All Notes** — search, filter by mood, and jump to any date across all diary entries.
- **Water tracker** — log glasses of water (250ml each). Auto-ticks the water habit when you hit 2500ml. Shows a 7-day bar chart and streak.
- **Holidays manager** — mark single days or date ranges as holidays or special working days. The app auto-detects which schedule to show for any date.
- **Pomodoro timer** — 25-minute focus timer built into every learning block.
- **Daily snapshot** — one tap generates a text summary of today (focus, water, habits, schedule) that you can copy and paste anywhere.
- **Export / Import** — full data backup as JSON. Restore on any device.
- **Dark mode** — toggle between light and dark themes.

---

## How to use

### Option 1 — Run locally (no internet needed)

1. Download `index.html` from this repository
2. Open it in Chrome by double-clicking
3. Bookmark it for quick daily access
4. All data is saved in your browser automatically

### Option 2 — Access from any device via GitHub Pages

Open the live URL in any browser on any phone or computer:

```
https://your-username.github.io/tracker
```

Add to your phone home screen for a native app feel:
- **Android (Chrome):** Three-dot menu → Add to Home Screen
- **iPhone (Safari):** Share button → Add to Home Screen

---

## Data storage

All your personal data (habits, diary entries, tracker history, schedule changes) is stored in your browser's **localStorage**. It never leaves your device and is not uploaded anywhere.

> **Important:** Data is tied to the specific browser on the specific device. Use the Export button regularly to download a backup JSON file. Use Import to restore on a new device.

---

## Backup and restore

| Action | How |
|--------|-----|
| Back up your data | Open app → top bar → **↓ Export** → saves `habit_backup_YYYY-MM-DD.json` |
| Restore data | Open app → top bar → **↑ Import** → select your backup file |
| Move to new device | Export on old device → copy JSON file → Import on new device |

---

## Features at a glance

| Feature | Details |
|---------|---------|
| Schedule tabs | Mon / Tue / Wed / Thu / Fri / Weekend — each separate and editable |
| Time block editing | Edit time, label, description, colour. Move up/down. Delete. |
| Duplicate block | Copy a block to another day when adding |
| Pomodoro timer | 25-min countdown on any learning block |
| Habit tracker | Done / Skip / Empty per habit per day |
| Per-habit notes | Add notes to any habit on any day |
| Monthly % | Shows last-30-day completion rate per habit |
| Pause habits | Exclude a habit from a date range (travel, etc.) |
| Streak counter | Consecutive days all habits completed |
| Milestones | Celebrations at 7, 14, 30 perfect days |
| Weekly summary | Auto-generated best day, worst day, score, advice |
| Heatmap | 6 months of daily habit consistency |
| Diary | Daily journal with mood tags |
| All Notes | Search + mood filter + date jump across all entries |
| Water tracker | 10 glass icons, 7-day chart, auto-ticks water habit |
| Daily focus | One-line priority saved per day |
| Daily snapshot | Copy today's summary as plain text |
| Holiday manager | Single day or date range, auto-skips weekends in ranges |
| Indian holidays | 2026–2027 preset quick-add buttons |
| Auto schedule detection | App opens correct day tab automatically |
| Dark mode | Full dark theme, saved across sessions |
| Export / Import | JSON backup, works across devices |
| Offline | Works completely without internet |
| No account needed | No login, no server, no cloud |

---

## Schedule logic

| Day | Schedule used |
|-----|--------------|
| Monday | Monday tab (includes extra 9–10 PM call) |
| Tuesday | Tuesday tab |
| Wednesday | Wednesday tab (includes extra 9:30–10 PM call) |
| Thursday | Thursday tab (includes extra 9–10 PM call) |
| Friday | Friday tab |
| Saturday / Sunday | Weekend / Holiday tab |
| Any day marked as Holiday | Weekend / Holiday tab |
| Any day marked as Working day | Weekday schedule for that day |

---

## Tracking starts from

**April 20, 2026** — streak and heatmap calculations begin from this date.

---

## How to update

When a new version is available:

1. Export your data backup first (top bar → Export)
2. Download the new `index.html`
3. In your GitHub repository, delete the old `index.html` and upload the new one
4. GitHub Pages rebuilds automatically within 1–2 minutes
5. Your data is unaffected (it lives in the browser, not in the file)

---

## Files in this repository

| File | Description |
|------|-------------|
| `index.html` | The complete app — open this in any browser |
| `README.md` | This file |

---

## Tech stack

Pure HTML, CSS, and vanilla JavaScript. No frameworks. No dependencies. No build step. Everything is in one file.

Data persistence uses `localStorage` in the browser. The storage key is `nara_v6`.

---

## Default habits

The app comes pre-loaded with these 11 habits:

1. No phone on waking — first 30 min screen-free
2. Morning walk — at least 20 min
3. Big Data / DE course — weekdays 9:30 AM / weekends 10:30 AM
4. Finance study — min 30 min
5. 2.5 L water — tracked through the day (auto-ticks from water widget)
6. 20-20-20 eye rule — every 20 min at screen
7. No Instagram before 7 PM — keep the rule
8. Evening walk — at least 30 min
9. Screen-free dinner — no phone at table
10. Wind-down routine — prayer / reflection before sleep
11. Asleep by 10:30 PM — protect sleep window

All habits can be edited, deleted, reordered, or paused in the **Manage Habits** tab.

---

## Privacy

- No data is ever sent to any server
- No analytics, no tracking, no cookies
- No account required
- Everything stays in your browser

---

*Built for personal use. Tracking habits, learning, finance, and daily life from April 20, 2026.*

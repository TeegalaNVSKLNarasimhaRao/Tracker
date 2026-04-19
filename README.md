# My Schedule & Habit Tracker

A personal productivity app — daily schedule, habits, work log, diary, finance tracking, and insights — synced across all devices via Firebase.

**Live:** https://teegalanvsklnarasimharao.github.io/Tracker/

---

## Setup

1. **Clone / download** `index.html` from the repository
2. **Push to GitHub Pages** — the file is entirely self-contained (no build step)
3. **Firebase** is already configured. Each Google account gets its own private data space

---

## Features

| Tab | What it does |
|-----|-------------|
| **Schedule** | Day-by-day timetable (Mon–Fri + Weekend). Drag to reorder blocks, save/apply templates, reset to defaults |
| **Tracker** | Weekly habit grid. Tick habits, add notes per cell, view 12-week trend chart |
| **Habits** | Add/edit/delete habits, pause habits for date ranges |
| **Heatmap** | 6-month visual habit consistency calendar |
| **Diary** | Daily journal with mood tags, auto-save, search |
| **Work Log** | Day/week work entry log with project tracking and time summaries |
| **All Notes** | Full diary search, mood filter, go-to-date |
| **Insights** | Monthly stats: habit rate, perfect days, diary words, water goals, mood breakdown |
| **Finance** | Income / expense / investment / saving tracker with monthly savings goal bar |
| **Holidays** | Mark holidays and override schedule type for any date |

### Always-on widgets
- **Daily check-in** — morning habit rating (1–5) + blocker note, auto-expands 6–11 AM
- **Today's focus** — single daily priority, collapsible
- **Water tracker** — 10-glass tracker with 7-day history chart, auto-ticks habit at 2.5L
- **Pomodoro timer** — launches from any learning block

---

## Usage

### Sign in
Click **Sign in with Google**. Your data is completely private per Google account.

### Schedule
- Click a **day tab** to view that day's schedule
- **+ Add time block** — enter time (e.g. `9:30-11:30 AM`), label, colour category. Conflict detection warns if a time slot overlaps an existing block
- **✎ Edit / Del** buttons on each block
- **⠿ Drag handle** — drag blocks to reorder
- **↺ Reset day** — restores the day to your account's default schedule
- **💾 Save as template** / **📄 Apply template** — save and reuse schedule patterns

### Habits
- Tick habits in the Tracker tab (click cell: empty → done ✓ → skipped — → empty)
- Add a note to any cell via the **+** icon
- Streak counter uses grace-day logic: one missed day per 7 consecutive days doesn't break your streak

### Diary
- Navigate with ← → arrows or **Today** button
- **Ctrl+S** saves the current entry
- Entries auto-save after 30 seconds of inactivity

### Work Log
- Day view: log entries with start time, duration, project, task, status
- Week view: summary table + copy-to-clipboard
- Quick-fill chips populate task from today's schedule blocks

### Finance
- Add income, expense, investment, or saving entries per month
- Set a monthly savings goal to see progress bar
- Navigate months with ← → buttons and **This month**

### Keyboard shortcuts (when not in a text field)
| Key | Action |
|-----|--------|
| `J` | Previous day (Diary / Work Log) |
| `K` | Next day |
| `T` | Jump to today |
| `N` | New work log entry / focus diary input |
| `?` | Show shortcut hint |
| `Ctrl+S` | Save diary entry |

---

## Data & Privacy
- All data is stored in **Firebase Firestore** under your Google UID — no one else can access it
- **Export** downloads a full JSON backup
- **Import** merges a backup file into your current data
- Water and focus history is pruned to 60 days to keep Firestore docs small
- Work log entries older than 90 days are archived as monthly summaries

---

## Changes in v14

### Bugs Fixed
| # | Issue | Fix |
|---|-------|-----|
| C1 | All Notes tab crashed when weekly review was saved (boolean stored in diary) | Filter non-object diary entries; store sentinel in `S.checkin` |
| C2 | Review sentinel key polluted All Notes list | Sentinel moved to `S.checkin[date+'_review']` |
| C3 | Weekly review text saved with literal newline | Join uses `\n` string |
| C4 | Finance delete crashed (`.filter()` on object) | `Array.isArray` guard added |
| C5 | Finance delete targeted wrong month | `data-fmo` attribute passes original month |
| C6 | `initDragDrop()` called but not defined | Phantom call removed; `attachDragHandlers()` used |
| C7 | `checkinOpen` / `_kbAttached` undeclared in strict mode | Declared as module-level `let` variables |
| C8 | `renderInsights` crashed on old diary entries without `.text` | `e&&e.text` guard added |

### UI/UX Fixes (this release)
| # | Issue | Fix |
|---|-------|-----|
| U1 | **"− hide" button overlapped "Save" button** in focus widget | Moved hide button into flex row alongside Save; removed `position:absolute` |
| U2 | **"View today →" button did nothing visibly** | Handler confirmed + `window.scrollTo({top:0})` added |
| U3 | **Owner's default schedule not showing** | `loadFromFirebase` now resets any day with < 4 blocks to owner defaults |
| U4 | **No time conflict warning** when adding overlapping blocks | Full time parsing + overlap detection with inline warning and save-anyway confirm |
| U5 | **No way to recover default schedule** | "↺ Reset day" button added to schedule toolbar |
| U6 | Tabs overflowed and wrapped on mobile | `overflow-x:auto; flex-wrap:nowrap` on tabs row |
| U7 | Responsive CSS gaps on very small screens | Extra `@media` breakpoints at 480px and 380px |

---

## File Structure

```
index.html          — entire app (single file, no dependencies except Firebase CDN)
test_tracker.js     — browser console test suite (paste & run runAllTests())
README.md           — this file
```

---

## Running Tests

1. Open the live app and sign in
2. Open browser DevTools → Console
3. Paste the contents of `test_tracker.js`
4. The tests run automatically, or call `runAllTests()`

Expected output: all green ✅. Failed tests print in red with details.

---

## Firebase Security Rules

Ensure Firestore rules restrict documents to the authenticated user:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/data/{docId} {
      allow read, write: if request.auth != null
        && request.auth.uid == userId
        && docId in ['meta', 'tracker', 'diary'];
    }
  }
}
```

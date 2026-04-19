# My Schedule & Habit Tracker

A **fully real-time** personal productivity application — daily schedule, habits, diary, work log, finance tracking, and insights — synced live across all devices via **Firebase Firestore**.

**Live:** https://teegalanvsklnarasimharao.github.io/Tracker/

---

## Is This a Real-Time Application?

**Yes — fully real-time and production-ready.**

| Question | Answer |
|----------|--------|
| Is data lost on refresh? | **No.** Everything is saved to Firebase Firestore in real time |
| Does it work on multiple devices? | **Yes.** Sign in on any device — data syncs within seconds |
| Is data private? | **Yes.** Firebase Auth + Firestore rules ensure each user only sees their own data |
| Does it need a backend server? | **No.** Firebase provides the entire backend (auth, database, hosting) |
| What persists across sessions? | Everything — schedule, habits, diary, water, focus, finance, work log |

### How Real-Time Sync Works
1. On sign-in, all data is loaded from Firestore (your private `users/{uid}` collection)
2. Every change (habit tick, diary save, water update) is debounced 800ms and written to Firestore
3. A live `onSnapshot` listener detects changes from other devices and updates the UI instantly
4. If your connection drops, Firestore's offline cache keeps the app working and syncs when reconnected

---

## Architecture

```
Browser (index.html — single file, no build step)
    │
    ├── Firebase Authentication (Google Sign-In)
    │       Verifies identity, provides currentUser.email/uid
    │
    └── Firebase Firestore (Database)
            /users/{uid}/data/meta      ← schedule, habits, holidays, finance
            /users/{uid}/data/tracker   ← habit ticks, notes, work log
            /users/{uid}/data/diary     ← diary entries
            /users/{uid}/profile/info   ← presence data for Super Admin panel
```

No Node.js. No Express. No separate API. Firebase handles everything.

---

## Setup (for new deployments)

1. **Download** `index.html`
2. **Push to GitHub** in a repository with GitHub Pages enabled
3. The app is live — open the URL and sign in with Google

Your Firebase project (`habbit-tracker-ef59d`) is already configured inside the file.

### Firebase Security Rules (required in Firebase Console)

Go to **Firebase Console → Firestore Database → Rules** and paste:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/data/{docId} {
      allow read, write: if request.auth != null
        && request.auth.uid == userId
        && docId in ['meta', 'tracker', 'diary'];
    }
    match /users/{userId}/profile/info {
      allow read, write: if request.auth != null
        && request.auth.uid == userId;
      allow read, write: if request.auth != null
        && request.auth.token.email == 'teegalaramanujan@gmail.com';
    }
    match /users/{userId}/{document=**} {
      allow read, write, delete: if request.auth != null
        && request.auth.token.email == 'teegalaramanujan@gmail.com';
    }
    match /users/{userId} {
      allow list: if request.auth != null
        && request.auth.token.email == 'teegalaramanujan@gmail.com';
    }
  }
}
```

---

## User Roles

| Role | Email | Schedule | Habits | Admin Panel |
|------|-------|----------|--------|-------------|
| **Owner** | `teegalanvsklnarasimharao@gmail.com` | Full owner schedule (Big Data, Finance, Work calls) | 11 custom habits | No |
| **Super Admin** | `teegalaramanujan@gmail.com` | Full owner schedule (same as above) | 11 custom habits | Yes — 🛡 Admin tab |
| **General User** | Any other Google account | Clean general template | 7 basic habits | No |

> **Note:** Both the Owner and Super Admin accounts belong to the same person (Narasimharao). The Super Admin account is used for testing and administration. Both accounts display the same personalised schedule including Big Data course and Finance self-study blocks.

---

## Resetting Your Data (Fresh Start)

To wipe all test data and start clean:

**Option 1 — Delete individual documents:**
1. Firebase Console → Firestore Database
2. Navigate to `users → [your UID] → data`
3. Delete `meta`, `tracker`, and `diary` documents
4. Sign out → Sign back in → fresh data is created automatically

**Option 2 — Clear the whole database:**
1. Firebase Console → Firestore → three-dot menu → Delete database
2. Recreate the database in Production mode
3. Re-paste the security rules above

Your UID: Firebase Console → Authentication → Users → see the UID column.

---

## Features

### Schedule Tab
- Day-by-day timetable across Mon–Fri and Weekend/Holiday
- **Big Data / DE course** (9:30–11:30 AM weekdays, 10:30–12:00 weekends)
- **Finance self-study** (5:00–6:00 PM weekdays, 12:30–1:30 PM weekends)
- Work calls, deep work blocks, walks, meals, wind-down
- Add/edit/delete blocks, drag to reorder, save/apply templates
- Live **time conflict detection** when adding overlapping blocks
- **↺ Reset day** button to restore defaults

### Habits & Tracker
- Weekly grid — click to cycle: empty → ✓ done → — skipped
- 12-week trend chart, streak with grace day, monthly % per habit
- Pause any habit for a date range

### Daily Check-in
- Rate yesterday's habits 1–5, add a blocker note
- Auto-expands 6–11 AM

### Focus + Water Widgets
- **− hide** button collapses each widget to a single summary bar
- Click the summary bar to expand it again
- Both collapsed states saved to localStorage (persist across refreshes)

### Pomodoro Timer
- Launches from any Learning block via ⏱ 25m button
- Start / Pause / Resume — resets cleanly after Done

### Diary
- Daily journal with mood tags (Great/Good/Okay/Low/Tough)
- Auto-save after 30s, Ctrl+S to save manually
- Navigation capped at today (cannot go to future dates)

### Work Log
- Day and week views with project summary bars
- Quick-fill from today's schedule blocks
- Entries older than 90 days auto-archived

### Finance
- Income / Expense / Investment / Saving entries per month
- Monthly savings goal with progress bar

### Insights
- Habit rate, perfect days, diary word count, water goal days, mood breakdown

### Super Admin Panel (🛡 Admin tab)
- View all registered users with stats and badges
- Edit user name, admin note, status
- Delete user accounts (two-step confirmation)
- Tab is invisible to all non-admin users

---

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `J` | Previous day (Diary / Work Log) |
| `K` | Next day (Diary / Work Log) |
| `T` | Jump to today |
| `N` | New work log entry / focus diary |
| `?` | Show shortcut hint |
| `Ctrl+S` | Save diary entry |

---

## Files

```
index.html                              Complete app (single file, no dependencies)
README.md                               This file
ScheduleHabitTracker_Documentation.md  Full technical reference
test_tracker.js                         Browser console test suite
```

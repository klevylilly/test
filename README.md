[README.md](https://github.com/user-attachments/files/26908397/README.md)
# Handoff: MedTracker — Medication Tracking App

## Overview
Six wireframe concepts for a mobile medication tracking app. The core goals are:
1. Make it easy for users to log whether they've taken their meds each day
2. Support custom reminders for complex medication schedules (tapers, every-N-hours, specific days, etc.)

---

## About the Design Files
The file `MedTracker Wireframes.html` is a **design reference created in HTML** — an interactive wireframe prototype showing intended layout, content, and behavior. It is **not** production code to copy directly.

Your task is to **recreate these designs in your target codebase** (React Native, SwiftUI, Android, React web, etc.) using its established patterns, component libraries, and navigation primitives.

---

## Fidelity
**Low-fidelity wireframes.** These are sketchy, rough layouts using a handwritten font (Caveat) and monochrome + limited-color palette. They show **structure, flow, and interaction model** — not final visual polish. Apply your codebase's existing design system (colors, typography, spacing, components) when implementing.

---

## Screens / Views

### Concept 1 — Big Tap (Home Screen)
**Purpose:** Daily med list. One tap toggles a med as taken.

**Layout:**
- Full-screen scrollable list
- Header: date label + subtitle
- Each medication = a card row (full width, ~70px tall)
  - Left: colored pill icon
  - Middle: med name (bold, 14px) + time (11px, muted)
  - Right: checkbox
- Card border + background color changes on tap (taken state)
- Footer: streak counter bar

**Interactions:**
- Tap card → toggle taken/not-taken
- Taken state: colored border, tinted background, green checkmark
- Untaken state: black border, white background, empty checkbox

---

### Concept 2 — Timeline (Home Screen)
**Purpose:** Vertical time-axis view. Meds are grouped by time of day.

**Layout:**
- Header: day + date
- Scrollable content area with left padding (~52px)
- Vertical line runs down left side (2px, light gray)
- Time slots (8:00 AM, 12:00 PM, 9:00 PM):
  - Time label pinned left of axis
  - Dot on axis (green if all taken, gray if not)
  - Med cards stacked vertically, right of axis
- Each med card: pill icon + name + checkbox
- Bottom tab bar: Today / History / Schedule / Settings

**Interactions:**
- Tap med card → toggle taken/not-taken
- Dot turns green when all meds in that slot are taken

---

### Concept 3 — Swipe to Log (Check-in Flow)
**Purpose:** One-at-a-time morning check-in. Reduces cognitive load to a single decision per med.

**Layout:**
- Header: session title + remaining count
- Card stack in center (shows current + ghost of next card behind it)
  - Current card: pill icon, name, dose, time
- Two buttons at bottom: "✕ Skip" and "✓ Taken"
- Log dots below buttons (one per completed decision)

**Interactions:**
- Tap "Taken" → log as taken, advance to next card
- Tap "Skip" → log as skipped, advance to next card
- When all done: completion state with next-dose time

---

### Concept 4 — Clock Wheel (Home Screen)
**Purpose:** Radial clock face showing dose times spatially. Gives instant sense of "time until next dose."

**Layout:**
- Clock face SVG (224×224): outer ring with hour ticks, dashed inner ring for dose track
- Dose dots placed at their time positions on the ring
  - Done: filled with med color + checkmark
  - Pending: white fill with "!" in med color
- Red hour hand showing current time
- Detail card below clock: shows selected dose info + "Mark taken" button

**Interactions:**
- Tap a dose dot → show detail card for that dose
- Tap again to deselect

---

### Concept 5 — Habit Grid (Home + History)
**Purpose:** Monthly calendar grid with color-coded adherence. Motivates through streaks and visual history.

**Layout:**
- Month title
- 7-column grid (Sun–Sat), 2 empty cells offset for April
- Each day cell: small square, color-coded
  - Green = all taken
  - Yellow = some taken
  - Red = missed
  - Gray = future
  - Today: white with blue border, tappable
- Legend row below grid
- Today's med list with checkboxes (bulk-toggle via grid tap)
- Adherence % banner at bottom

**Interactions:**
- Tap today's cell → toggle all meds for today as taken/untaken

---

### Concept 6 — Schedule Builder (Two-tab View)
**Purpose:** Focused on supporting complex regimens. Tab 1 = today's doses, Tab 2 = schedule rules editor.

**Layout — Today tab:**
- Greeting + dose count
- Med cards (same pattern as Concept 1)
- "Next dose" countdown banner

**Layout — My Schedule tab:**
- List of medications, each showing its schedule rule(s)
  - e.g. "2×/day with meals · 8 AM + 6 PM"
  - e.g. "Taper: 3→2→1 weekly"
  - e.g. "Every 8 hrs · For 10 days"
- Edit button per med
- "+ Add medication" button
- Schedule type picker chips: Daily / Specific days / Every N hours / Taper / As needed

**Interactions:**
- Tab switch: Today ↔ My Schedule
- (Edit flow not yet designed — next step)

---

## Design Tokens (wireframe values — replace with your design system)

| Token | Value |
|---|---|
| Accent Blue | `#4a90d9` |
| Accent Green | `#5bba87` |
| Accent Orange | `#e07b54` |
| Accent Purple | `#9b6dd9` |
| Accent Yellow | `#f5c842` |
| Text primary | `#1a1a1a` |
| Text secondary | `#888` |
| Text muted | `#bbb` |
| Background | `#fff` |
| Canvas bg | `#f2f0eb` |
| Font (wireframe) | Caveat (handwritten) — replace with your system font |

---

## State Management

Each screen needs:
- `medications[]` — list of meds with name, dose, times, color, schedule rules
- `logEntries[]` — per-day records of taken/skipped per med
- `streakCount` — consecutive days with full adherence

Concepts 3 (Swipe) also needs:
- `currentCheckInIndex` — pointer into today's pending meds

Concept 6 schedule rules need a flexible schema, e.g.:
```
{
  type: 'daily' | 'specific_days' | 'every_n_hours' | 'taper' | 'as_needed',
  times: ['08:00', '21:00'],
  days?: [0,1,2,3,4,5,6],
  intervalHours?: 8,
  taperSchedule?: [{dose: 3, weeks: 1}, {dose: 2, weeks: 1}, {dose: 1, weeks: 1}],
  courseDays?: 10,
}
```

---

## Recommended Next Steps
1. Pick 1–2 concepts to combine (e.g. Concept 1 home + Concept 6 schedule builder)
2. Design the reminder/notification setup flow
3. Design the "add medication" flow
4. High-fidelity pass with final visual polish

---

## Files
- `MedTracker Wireframes.html` — interactive prototype with all 6 concepts (open in browser)

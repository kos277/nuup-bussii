[README.md](https://github.com/user-attachments/files/27176868/README.md)
# Nuup Bussii+ Transit App

A simple, self-contained bus timetable app for Nuuk, Greenland. No downloads, no servers, just open the HTML file and go.

## Features

- 🗺️ **Interactive Map** — All 70+ bus stops on one map
- 🚌 **Real Timetables** — All 5 routes (R1, R2, R3, RX2, RX3) with complete schedules
- ⏱️ **Smart Scheduling** — Weekday/weekend detection + holiday awareness
- ❤️ **Saved Stops** — Your favorite routes, always accessible
- 🌧️ **Weather Widget** — Check conditions before heading out
- ⏰ **Live Countdown** — See how many minutes until the next bus
- 📱 **Mobile-Friendly** — Works on phone, tablet, or desktop
- 🛠️ **Admin Panel** — Edit timetables, correct stop coordinates
- 💾 **Data Export/Import** — Backup and restore timetables as JSON

## Quick Start

### Option 1: GitHub (Recommended)
1. Clone: `git clone https://github.com/kos277/nuup-bussii.git`
2. Navigate: `cd nuup-bussii`
3. Open: `nuup-bussii-v5.html` in your browser
4. Done! All timetables load automatically.

### Option 2: Local Folder
If opening locally without Git, create this structure:
```
project-folder/
├── nuup-bussii-v5.html
└── backups/
    └── data.js
```
Then open `nuup-bussii-v5.html` in your browser.

Everything works offline after the first load.

## How to Use

### Finding a Bus

1. **Look at the map** — Colored dots are bus stops (numbered)
2. **Click any stop** — The bottom sheet shows departures for that stop
3. **See times** — Next bus is highlighted in blue with countdown (e.g., "12:38 (5m)")
4. **Tap again** — Expand to full schedule

### Save Your Favorite Stops

1. **Click a stop** to open it
2. **Tap the ★ button** to save
3. **Later:** Tap ★ again to see your saved stops
4. Favorites are stored in your browser

### Check Weather

Your **current conditions** (temp, wind) appear when you open the app. If gusts exceed 65 km/h, consider alternatives.

### Change the Schedule

**Top right:** Use the date and time pickers to jump to any weekday/weekend/holiday schedule. Times update automatically.

## Admin Panel

**Only for maintainers.** Click the **Admin** button (⚙️) in the top right.

### Stops Tab

- **Interactive map** with draggable pins for each stop
- **Drag to correct** stop location on the map
- **Click a pin** to see its ID and details
- **Save corrections** — automatically persisted to browser
- **Export** corrected stops as `stops.js`

### Timetables Tab

- **Select a route** (R1, R2, R3, RX2, RX3) with route-selector buttons
- **Select the day type** (Weekday or Weekend)
- **View or edit** trip times in an interactive grid
- **Add/remove trips** directly in the editor
- **Import new data** using the modal (accepts JSON or text format)

### Data Tab

- **Export all timetables + stops** as a single `data.js` file
- **Perfect for:** Backups, version control, sharing updates
- **Steps:**
  1. Admin → Data → "Export data.js"
  2. Save to: `backups/data.js` in your repo
  3. Commit to GitHub
  4. Users reload the page → instantly get updated data

## Timetable Import

### JSON Format (Easiest)

Paste your entire `timetables.json` export directly:

```json
{
  "timetables": {
    "R1": {
      "label": "Route 1",
      "color": "#ff6b9d",
      "data": {
        "weekday": {
          "stops": [18, 1, 47, 63, ...],
          "trips": [
            ["05:49", "05:50", "05:53", ...],
            ["06:09", "06:10", "06:13", ...]
          ]
        },
        "weekend": { ... }
      }
    },
    "R2": { ... },
    ...
  }
}
```

Just paste it into the import box. The app handles the rest!

### Text Format (Alternative)

If you have formatted text:

```
R1|weekday
18,1,47,63,50,54,56,57,60,61,41,64,46,8,9,52,28,27,62,58,24
05:49 05:50 05:53 05:54 05:56 05:58 06:00 06:02 06:03 06:05 06:07 06:09 06:10 06:12 06:13 06:15 06:18 06:19 06:21 06:22 06:24
06:09 06:10 06:13 06:14 06:16 06:18 06:20 06:22 06:23 06:25 06:27 06:29 06:30 06:32 06:33 06:35 06:37 06:38 06:42 06:44 06:47

R1|weekend
18,1,47,63,50,54,56,57,60,61,41,64,46,8,9,52,28,27,62,58,24
07:49 07:50 07:53 07:54 ...
```

Each block:
- **Line 1:** `ROUTEID|DAY` (R1|weekday, R1|weekend, R2|weekday, etc.)
- **Line 2:** Stop IDs in order (comma-separated)
- **Line 3+:** One trip per line (departure times, space-separated)

## Routes & Colors

| Route | Color | Serves | Schedule |
|-------|-------|--------|----------|
| **R1** | 🔴 Pink | Full circle | Weekday & Weekend |
| **R2** | 🟡 Yellow | Full circle | Weekday & Weekend |
| **R3** | 🟢 Green | Full circle | Weekday & Weekend |
| **RX2** | ⚫ Grey | Express | Weekday only |
| **RX3** | 🟠 Orange | Express | Weekday only |

## Offline Mode

This app works **100% offline** after the first load:
- Map tiles are cached in your browser
- Timetables loaded from `backups/data.js` (no fetch needed)
- All edits saved locally
- Weather updates when you reconnect (optional)

Perfect for underground or outside coverage areas.

## Troubleshooting

**Times seem wrong?**
- Check the date/time picker (top right) — verify you're on the correct day and schedule (weekday/weekend)
- Check holidays: 01-01, 01-06, 05-01, 06-21, 12-24, 12-25, 12-26, 12-31 follow weekend schedule

**Stop doesn't show times?**
- The stop might not be served by that route. Check the admin panel timetables.
- Or: The timetable data for that route hasn't been imported yet.

**Folder structure error?**
- If opening locally, ensure you have: `nuup-bussii-v5.html` + `backups/data.js` in the correct folder
- From GitHub: Just clone and open — everything is already set up

**Favorites disappeared?**
- They're stored in your browser's local storage. Clearing cache/cookies will delete them.
- **Backup:** Admin → Data → Export `data.js` includes any saved stops

**Map won't load?**
- You need internet the **first time** to download map tiles from OpenStreetMap
- After that, tiles are cached and work offline

**Browser compatibility?**
- Works best on: Chrome, Firefox, Safari, Edge (modern versions)
- Requires: JavaScript enabled, localStorage support

## Technical Details

- **Architecture:** Single HTML file (no build step, no dependencies)
- **Data loading:** `<script src="backups/data.js">` — instant, offline
- **Maps:** Leaflet.js 1.9.4 (OpenStreetMap tiles)
- **Weather:** Open-Meteo API (free, no key)
- **Storage:** Browser localStorage for favorites, edits, stop corrections
- **Timezone:** America/Godthab (UTC-3, Greenland)

## Source Code

Full architecture, data structures, and code comments are in the HTML file header comment. Open `nuup-bussii-v5.html` in a text editor to see the complete context.

## Development

See **DEVELOPMENT.md** for:
- How to add features
- Git workflow
- Testing checklist
- Working with Claude for updates

## GitHub

Repository: [github.com/kos277/nuup-bussii](https://github.com/kos277/nuup-bussii)

---

**Made for Nuuk commuters. Open source. No ads. No tracking.**

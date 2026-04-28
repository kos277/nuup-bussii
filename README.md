# Nuup Bussii+ Transit App

A simple, self-contained bus timetable app for Nuuk, Greenland. No downloads, no servers, just open the HTML file and go.

## Features

- 🗺️ **Interactive Map** — All 70+ bus stops on one map
- 🚌 **Real Timetables** — All 5 routes (R1, R2, R3, RX2, RX3)
- ⏱️ **Smart Scheduling** — Weekday/weekend detection
- ❤️ **Saved Stops** — Your favorite routes, always accessible
- 🌧️ **Weather Widget** — Check conditions before heading out
- ⏰ **Live Countdown** — See how many minutes until the next bus
- 📱 **Mobile-Friendly** — Works on phone, tablet, or desktop
- 🛠️ **Admin Panel** — Edit timetables without re-scraping

## Quick Start

1. **Download** `nuup-bussii-v5.html`
2. **Open** in your browser (double-click the file)
3. **Use** the map to find stops, or use the date picker to change schedules

That's it. Everything works offline.

## How to Use

### Finding a Bus

1. **Look at the map** — Colored dots are bus stops
2. **Click any stop** — The bottom sheet shows departures
3. **See times** — Next bus is highlighted in blue with countdown

### Save Your Favorite Stops

1. **Click a stop** to open it
2. **Tap the ★ button** to save
3. **Tap the handle** to collapse to peek mode
4. **Your favorites appear at the top**

### Check Weather

Your **current conditions** (temp, wind) appear in the peek state. If gusts exceed 65 km/h, consider taking a taxi.

### Change the Schedule

**Top right:** Use the date and time pickers to jump to any weekday/weekend schedule. Times adjust automatically.

## Admin Panel

**Only for maintainers.** Click the **Admin** button.

### Timetables Tab

- **Select a route** (R1, R2, R3, RX2, RX3)
- **Select the day type** (Weekday or Weekend)
- **Edit trip times** directly in the grid
- **Import new data** using the formatted import modal
- **Export data** as JSON for backups

### Import Format

If you need to update timetables:

```
R1|weekday
18,1,47,63,50,54,56,57,60,61,41,64,46,8,9,52,28,27,62,58,24
05:49 05:50 05:53 05:54 05:56 05:58 06:00 06:02 06:03 06:05 06:07 06:09 06:10 06:12 06:13 06:15 06:18 06:19 06:21 06:22 06:24
06:09 06:10 06:13 06:14 06:16 06:18 06:20 06:22 06:23 06:25 06:27 06:29 06:30 06:32 06:33 06:35 06:37 06:38 06:42 06:44 06:47
```

Each block is:
- **Line 1:** `ROUTEID|DAY` (e.g., R1|weekday)
- **Line 2:** Stops in order (comma-separated IDs)
- **Line 3+:** One trip per line (times separated by spaces)

## Routes & Colors

| Route | Color | Runs | Service |
|-------|-------|------|---------|
| **R1** | 🔴 Pink | Every route | Weekday & Weekend |
| **R2** | 🟡 Yellow | Every route | Weekday & Weekend |
| **R3** | 🟢 Green | Every route | Weekday & Weekend |
| **RX2** | ⚫ Grey | Weekday only | Weekday |
| **RX3** | 🟠 Orange | Weekday only | Weekday |

## Offline

This app works entirely **offline**. Once loaded, you don't need internet — even maps work without a connection (cached tiles). Perfect for when you're underground or outside the network.

## Troubleshooting

**Times seem wrong?**
- Check the date/time picker (top right) — make sure you're on the right day/schedule

**Stop doesn't show times?**
- The stop might not serve that route. Check the admin panel to verify timetables are imported.

**Favorites disappeared?**
- They're stored in your browser. If you clear cache/cookies, they'll be lost. Export a backup from the admin panel.

**Map won't load?**
- You need internet the first time to download map tiles. After that, it uses cached tiles.

## Technical Details

- **Single HTML file** — No installation, no backend
- **Leaflet.js** — Maps library
- **Open-Meteo API** — Weather data (no key required)
- **Browser Storage** — Favorites and edits saved locally
- **Works on:** Chrome, Firefox, Safari, Edge (modern versions)

## Source Code

Full architecture, data structures, and code comments are in the HTML file header. Open `nuup-bussii-v5.html` in a text editor to see them.

## Feedback

Found a bug? Want a feature? The code is on GitHub — open an issue or contact the maintainer.

---

**Made for Nuuk commuters. By Søren & Claude.**
# nuup-bussii

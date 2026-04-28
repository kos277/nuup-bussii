[DEVELOPMENT.md](https://github.com/user-attachments/files/27176903/DEVELOPMENT.md)
# Development Guide

## Your Workflow (Office Network)

### Starting a New Session

When you have a feature request or bug fix:

1. **Open `nuup-bussii-v5.html` in a text editor**
2. **Copy the header comment** (the long comment at the very top with architecture info)
3. **Start a new chat** with Claude
4. **Paste the header comment** into the chat
5. **Paste the entire HTML file** (optional, but helpful for context)
6. **Describe what you want:**
   ```
   "I want to add X feature"
   "I found a bug: Y happens when Z"
   "Update timetables for route R1"
   ```

### Getting the Updated Code

Claude will:
1. Read the header comment → instant context
2. Update the HTML file
3. Provide the updated file in the output

You:
1. **Download** the updated HTML
2. **Test locally** in your browser (just open the file with folder structure)
3. **Verify** the feature works using the testing checklist (in header comment)

### Local Testing Setup

Before testing, ensure your folder structure:
```
project-folder/
├── nuup-bussii-v5.html        ← Your HTML file
└── backups/
    └── data.js                 ← Timetables data (included via script tag)
```

This is required because the HTML loads data via `<script src="backups/data.js">`.

### Committing to GitHub

```bash
# Navigate to your repo
cd ~/path/to/nuup-bussii

# See what changed
git status

# Stage the updated file
git add nuup-bussii-v5.html

# (Optional) If you exported new timetables
git add backups/data.js

# Commit with clear message
git commit -m "feat: Add feature name"
# or
git commit -m "fix: Bug description"
# or  
git commit -m "docs: Update header comment"

# Push to GitHub
git push origin main
```

### Version Numbers

Keep it simple:
- **v5.0** — Initial release
- **v5.1** — First update
- **v5.2** — Second update
- **v6.0** — Major redesign (later)

Only tag releases when stable:
```bash
git tag v5.1
git push origin --tags
```

## Data Flow: From Timetables to Users

### The Complete Workflow

1. **You receive timetables** (PDF, JSON, etc. from bus.gl)
2. **Import into admin panel** (Admin → Timetables → Import)
3. **Export as `data.js`** (Admin → Data → Export)
4. **Save to repo** (move file to `backups/data.js`)
5. **Commit to GitHub**
6. **Users reload page** → instantly get fresh data (no fetch needed)

### Why `backups/data.js`?

- **Performance:** Included via `<script>` tag at page load (0ms vs API fetch)
- **Offline:** No network request needed
- **Reliability:** No API failures, no CORS issues
- **Control:** You manage exactly what data is in the app

## Common Scenarios

### Scenario: Update Timetables

**Before:**
- Times were hardcoded in HTML
- Users needed to wait for API fetch
- Risk of network failures

**Now:**
```
1. Get new timetables (JSON or PDF)
2. Admin → Timetables → Import (paste JSON or text)
3. Admin → Data → Export data.js
4. Save to: backups/data.js
5. git add backups/data.js && git commit && git push
6. Users reload → get new times instantly ✓
```

**Test before committing:**
- Check 3-5 stops with the new times
- Verify weekday/weekend schedules differ
- Confirm no times are missing

### Scenario: Add a Feature

1. Describe feature to Claude (with header comment)
2. Get updated HTML
3. Test locally with proper folder structure
4. Commit: `git commit -m "feat: description"`

### Scenario: Fix a Bug

1. Reproduce the bug locally
2. Ask Claude with details
3. Test the fix
4. Commit: `git commit -m "fix: bug description"`

### Scenario: Sync from Home (Future)

If you're working from home and want to use Claude Code:

1. Clone the repo in Claude Code
2. Ask Claude to add the feature
3. Claude commits directly
4. You pull on your office machine if needed

**Note:** The header comment still helps! Claude Code reads it the same way chat Claude does.

## File Organization

```
nuup-bussii/
├── nuup-bussii-v5.html        ← Main app (has full context in header)
├── README.md                   ← User guide (update when UI changes)
├── DEVELOPMENT.md              ← This file (rarely changes)
├── .gitignore                  ← Standard ignores
├── .git/                       ← Git history (auto-managed)
└── backups/                    ← Timetable exports
    ├── data.js                 ← Current data (loaded via script tag)
    └── data-2026-04-28.json    ← Archive backups
```

## Testing Checklist

Before committing, verify:

- [ ] Folder structure exists: `nuup-bussii-v5.html` + `backups/data.js`
- [ ] HTML opens without errors
- [ ] Map loads with all stops (70+ dots)
- [ ] Click any stop → bottom sheet appears
- [ ] Shows correct stop name + stop number
- [ ] Shows all routes serving that stop
- [ ] Next bus displays with countdown (e.g., "12:38 (5m)")
- [ ] Expand sheet → shows full schedule for the day
- [ ] Admin panel opens/closes with ⚙️ button
- [ ] Admin → Stops: Interactive map with draggable pins
- [ ] Admin → Timetables: Route selection + day type buttons
- [ ] Admin → Timetables: Import accepts JSON paste
- [ ] Admin → Data: Export downloads `data.js`
- [ ] Favorites (★) save and persist
- [ ] Date picker switches weekday/weekend correctly
- [ ] Weather widget shows temp + wind (if online)
- [ ] No console errors (press F12 → Console tab)

## Git Habits

**Good commits:**
```bash
git commit -m "feat: Add export timetables button"
git commit -m "fix: Next bus countdown updates correctly"
git commit -m "docs: Update header comment version"
```

**Less helpful:**
```bash
git commit -m "update"
git commit -m "bug"
```

**View history:**
```bash
git log --oneline          # See recent commits
git diff HEAD~1            # See what changed last commit
git show v5.0              # See specific version
```

## Updates to Header Comment

The HTML header comment is **the source of truth**. When updating it, include:

- Current version number (top of comment)
- Last updated date
- New features in CURRENT STATUS section
- New limitations if any
- Update NEXT PRIORITIES if changed

Example:
```html
<!--
╔════════════════════════════════════════════════════════════════════════════╗
║                         NUUP BUSSII+ TRANSIT APP                          ║
║                                v5.1 ← UPDATED                             ║
║                   Last Updated: 2025-05-10 ← UPDATED                      ║
╚════════════════════════════════════════════════════════════════════════════╝
...
CURRENT STATUS:
  ✅ COMPLETE: All 5 routes imported
  ✅ WORKING: Data export/import (JSON support)
  ✅ WORKING: Offline timetables via backups/data.js
  ...
```

## When to Use Chat vs. Claude Code (Future)

**Chat (from office now):**
- Paste header comment
- Paste HTML
- Request feature
- Get updated file
- Test with folder structure
- Commit, push manually

**Claude Code (from home later):**
- Open repo
- Request feature
- Claude edits, commits automatically
- You pull/merge if needed

Same workflow, just fewer manual steps from home.

## Backup Strategy

Keep your work safe:

```bash
# After each session, backup locally
cp nuup-bussii-v5.html ~/backup/nuup-bussii-v5-$(date +%Y-%m-%d).html

# Or use GitHub (pushed every commit)
git push

# Export timetables regularly
# Admin → Data → Export → Save to backups/data-YYYY-MM-DD.json
```

## Long-term Maintenance

**Weekly:**
- Check if timetables need updates (if routes changed)

**Monthly:**
- Review bus.gl for schedule changes
- Update timetables if needed
- Export and commit `backups/data.js`

**Quarterly:**
- Review any feedback or issues
- Plan next features

**Yearly:**
- Full audit of app
- Update Leaflet.js if new version available
- Refactor code if needed

## Questions to Ask Claude Next Session

When you start a new chat, clarify:

```
"I want to [feature description]

Current state:
- v5.4 is stable
- All 5 routes fully populated
- JSON import working
- Offline data loading via backups/data.js

Does this require backward compatibility?"
```

This helps Claude understand the scope and constraints.

## Troubleshooting Development Issues

**"Map doesn't load"**
- Verify folder structure: `backups/data.js` exists
- Open console (F12) for errors
- Check network tab for failed requests

**"Import doesn't work"**
- Paste valid JSON (check syntax with online validator)
- Or use text format (see README for format)
- Check console (F12) for parsing errors

**"Timetables still empty after import"**
- Verify JSON structure matches expected format
- Check that route keys are exact: R1, R2, R3, RX2, RX3
- See console debug messages for import status

**"Changes not persisting"**
- localStorage might be full or disabled
- Check browser privacy/security settings
- Try exporting data as backup before troubleshooting

## Local Development Tips

**Live editing:**
- Edit HTML in text editor
- Refresh browser to see changes
- Keep console open (F12) to catch errors

**Testing different schedules:**
- Use date picker to test weekday vs weekend
- Test specific times with time picker
- Verify holiday dates (01-01, 01-06, 05-01, 06-21, 12-24, 12-25, 12-26, 12-31)

**Admin panel debugging:**
- Open console → watch for errors when importing
- Check Network tab to see if `backups/data.js` loads
- Use browser storage (F12 → Storage) to see saved data

---

**Bottom line:** Paste HTML + header comment. Describe what you want. Get updated file. Test with folder structure. Commit, push. Repeat.

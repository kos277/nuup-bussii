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
3. Paste the updated file in the chat output

You:
1. **Download** the updated HTML
2. **Test locally** in your browser (just open the file)
3. **Verify** the feature works using the testing checklist (in header comment)

### Committing to GitHub

```bash
# Navigate to your repo
cd ~/path/to/nuup-bussii

# See what changed
git status

# Stage the updated file
git add nuup-bussii-v5.html

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
- **v5.0** — Initial release (now)
- **v5.1** — First update
- **v5.2** — Second update
- **v6.0** — Major redesign (later)

Only tag releases when stable:
```bash
git tag v5.1
git push origin --tags
```

## Common Scenarios

### Scenario: Update Timetables

1. Get new PDF from bus.gl
2. Ask Claude to format it using the import prompt
3. Use Admin panel → Timetables → Import
4. Test 2-3 stops to verify times are correct
5. ✅ Done (no code commit needed if times only)
6. (Optional) Export to `backups/timetables-YYYY-MM-DD.json` and commit

### Scenario: Add a Feature

1. Describe feature to Claude
2. Get updated HTML
3. Test locally
4. Commit: `git commit -m "feat: description"`
5. (Optional) Update the header comment version number if significant change

### Scenario: Fix a Bug

1. Reproduce the bug locally
2. Ask Claude with details
3. Test the fix
4. Commit: `git commit -m "fix: bug description"`

### Scenario: Sync from Home

If you're working from home later and want to use Claude Code:

1. Clone the repo in Claude Code
2. Ask Claude to add the feature
3. Claude commits directly
4. Seamless sync

**Note:** The header comment still helps! Claude Code reads it the same way chat Claude does.

## File Organization

```
nuup-bussii/
├── nuup-bussii-v5.html        ← Main app (has full context in header)
├── README.md                   ← User guide (update when UI changes)
├── DEVELOPMENT.md              ← This file (rarely changes)
├── .gitignore                  ← Standard ignores
├── .git/                       ← Git history (auto-managed)
└── backups/                    ← Optional folder for exports
    └── timetables-2025-04-28.json
```

## Testing Checklist

Before committing, verify:

- [ ] Map loads with all stops
- [ ] Click any stop → sheet appears
- [ ] Shows correct stop name + stop number
- [ ] Shows all routes serving that stop
- [ ] Next bus displays with countdown (e.g., "12:38 (5m)")
- [ ] Admin panel opens/closes
- [ ] Admin → Timetables → routes selectable
- [ ] Admin → Timetables → import button works
- [ ] Favorites (★) save and delete
- [ ] Date picker switches schedules
- [ ] Weather widget shows temp + wind
- [ ] No console errors (press F12 to check)

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
  ✅ WORKING: Data export/import ← NEW FEATURE
  ...
```

## When to Use Chat vs. Claude Code (Future)

**Chat (from office now):**
- Paste header comment
- Paste HTML
- Request feature
- Get updated file
- Test, commit, push manually

**Claude Code (from home later):**
- Open repo
- Request feature
- Claude edits, commits automatically
- You pull/merge if needed

Same workflow, just fewer steps from home.

## Backup Strategy

Keep your work safe:

```bash
# After each session, backup locally
cp nuup-bussii-v5.html ~/backup/nuup-bussii-v5-$(date +%Y-%m-%d).html

# Or use GitHub (pushed every commit)
git push

# Or use cloud storage (Dropbox, Drive, etc.)
# Copy html + any exports to cloud folder
```

## Long-term Maintenance

**Monthly:**
- Check bus.gl for schedule changes
- Update timetables if needed

**Quarterly:**
- Review GitHub issues/feedback
- Plan next features

**Yearly:**
- Full audit of app
- Update Leaflet.js if new version available
- Refactor if needed

## Questions to Ask Claude Next Session

When you start a new chat, clarify:

```
"I want to [feature description]

Current state:
- v5.0 is stable
- All timetables imported
- Admin panel working

Does this require backward compatibility with existing data?"
```

This helps Claude understand the scope and constraints.

---

**Bottom line:** Paste HTML + header comment. Describe what you want. Get updated file. Test, commit, push. Repeat.

# Tome of Heroes — D&D 2024 Character Builder
## Project Brief for Claude Code

---

## What this is
A single-file (`index.html`) web app for building D&D 2024 (5.5e) character sheets. No backend, no framework — pure HTML/CSS/JS. Characters are saved to `localStorage`. Designed to be hosted on GitHub Pages.

---

## Current state
The app is fully functional with the following features:

### App UI (screen view)
- Dark fantasy aesthetic — parchment background, gold/blood-red accents, Cinzel + Crimson Pro fonts
- Persistent sidebar: character list, new/duplicate/delete/import/export actions
- 7 tabs: Core, Abilities, Combat, Spells, Features, Equipment, Backstory
- Responsive layout: collapses to single column on mobile (< 700px)
- Auto-saves to localStorage on every field change

### Tabs & content
- **Core**: name, race/subrace, class/subclass, background, alignment, level, XP, appearance, quick stats (AC, initiative, speed, prof bonus), proficiencies & languages
- **Abilities**: all 6 ability scores with correctly calculated modifiers (`Math.floor((score - 10) / 2)`), saving throws with proficiency checkboxes, all 18 skills with proficiency + expertise toggles, passive perception
- **Combat**: AC, initiative, speed, hit dice, HP tracker (max/current/temp), death saves (pip toggles), inspiration toggle, attacks table (name/bonus/damage/type, add rows), combat notes
- **Spells**: spellcasting ability selector, auto-calculated save DC and attack bonus, spell slot tracker (add/remove/expend per level), known spells list, spell picker with cantrips/1st/2nd level spells for: Wizard, Sorcerer, Warlock, Cleric, Druid, Bard, Paladin, Ranger
- **Features**: auto-populated class features filtered by level (all 13 classes), custom feature builder (name, description, source), personality traits/ideals/bonds/flaws
- **Equipment**: currency (cp/sp/ep/gp/pp), inventory textarea, treasure textarea
- **Backstory**: backstory, allies & organizations, notes

### Print sheet
- Hidden on screen, shown only during `window.print()`
- Mimics the official 2014 WotC character sheet layout
- 3-column layout:
  - Left: ability scores (with modifier + score), inspiration, proficiency bonus, saving throws, passive perception, skills (filled circles for proficiency)
  - Middle: AC/initiative/speed, HP block, death saves, attacks table, currency + equipment, optional spellcasting stats
  - Right: personality traits/ideals/bonds/flaws, features & traits, proficiencies & languages
- Uses `@media print` with `print-color-adjust: exact`
- Page size: US Letter, 0.35in margins

### Data included
- All races + subraces, all 13 classes + subclasses, backgrounds, alignments
- Class features for all 13 classes (up to level 9 or so)
- Spell lists (cantrips, 1st, 2nd level) for 8 spellcasting classes
- Proficiency bonus table for levels 1–20

---

## Known issues / planned improvements
- Spell lists only go to 2nd level — needs 3rd through 9th level spells added
- No automatic HP calculation from class + CON modifier
- No spell slot auto-population based on class + level
- No dice roller
- No character portrait / image upload
- No second sheet page for spells (official sheet has a separate spell sheet page)
- User accounts / cloud save not yet implemented (currently localStorage only)

---

## File structure
```
tome-of-heroes/
└── index.html       # entire app — HTML + CSS + JS in one file
```

Hosted on GitHub Pages at: `https://YOUR-USERNAME.github.io/tome-of-heroes/`

---

## Development conventions
- **Single file**: keep everything in `index.html` — no build tools, no npm, no external JS files
- **No frameworks**: vanilla JS only
- **Modifier formula**: `Math.floor((score - 10) / 2)` — do not use `||` default before subtraction
- **localStorage key**: `toh_chars_v2`
- **Character object shape**: see `blankChar()` function in the JS
- **Escaping**: always use the `esc()` helper before inserting user data into HTML strings
- **Print sheet**: rebuilt on every data change via `buildPrintSheet()` — keep it in sync with app data
- **Fonts**: loaded from Google Fonts (Cinzel, Crimson Pro) — requires internet connection

---

## How to work on this
```bash
# Clone your repo
git clone https://github.com/YOUR-USERNAME/tome-of-heroes.git
cd tome-of-heroes

# Open in browser for local testing
open index.html       # macOS
start index.html      # Windows

# After making changes
git add index.html
git commit -m "describe what changed"
git push
# GitHub Pages auto-deploys within ~60 seconds
```

---

## Suggested next tasks (pick up here)
1. Add 3rd–9th level spells for all spellcasting classes
2. Auto-populate spell slots by class + level on level change
3. Auto-calculate Max HP suggestion from class hit die + CON modifier
4. Add a dice roller panel (d4/d6/d8/d10/d12/d20/d100)
5. Add a second printable page mimicking the official spell sheet
6. Improve mobile layout — consider bottom nav bar instead of sidebar on small screens

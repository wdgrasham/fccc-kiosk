# FCCC Kiosk — Claude Startup Prompt
# ==========================================
# Boot sequence for Claude Cowork and Code sessions.
# Point your workspace folder here and say:
#   "Read CLAUDE-STARTUP.md and follow the instructions."
# ==========================================

## STEP 1 — READ THESE FILES (in this order)

Read every file listed below before writing code or making changes.

### Project rules (NEVER violate):
1. CLAUDE.md

### Specs and plans:
2. specs/KIOSK-REDESIGN-PLAN.md (THE master reference for V2 redesign — includes branding, class data, all groups)
3. specs/KIOSK-LOCKDOWN-GUIDE.md (device lockdown research — iPad, Android, Windows)

### Branding reference:
4. External Files/FirstColonyChurch_BrandingGuidlines2026.pdf (official brand guide — colors, fonts, logo rules, voice/tone)

### Tiri's feedback (raw source):
5. External Files/Kiosk Map of Options.docx (complete class data, content, structure)
6. External Files/Building Map Posters 2.pdf (updated building map from Tiri)

### Current source code:
4. index.html (the current alpha kiosk — single HTML file, ~1,673 lines)

---

## STEP 2 — CONFIRM STATE

After reading all files:

1. Run `git log --oneline -5` — show the last 5 commits
2. Confirm index.html exists and note its line count
3. List all files in assets/ (photos, maps, etc.)

Say: "Ready. Last commit: [hash] [message]. index.html is [X] lines.
[X] asset files found. Awaiting instructions."

---

## STEP 3 — CURRENT PRIORITIES

### V2 Redesign — Build Order (updated 2026-04-15):
- [x] **Group 1: Kiosk UI shell** — Home with 4 cards, no nav bar, back buttons,
  responsive, idle reset. Built 2026-04-15 by Bob.
- [x] **Group 2: Bible Classes tree** — Sunday/Wednesday → Adult/Children →
  class cards. Care Groups show monthly badge + schedule note. FriendSpeak shows
  3 session chips. Small Groups under Bible Classes. Built 2026-04-15 by Bob.
- [x] **Group 3: "New Here?" section** — Start Here, Sunday/Wednesday overviews,
  New Member. QR placeholders. Built 2026-04-15 by Bob.
- [x] **Group 4: Volunteer section** — Jump In, Opportunities, Spiritual
  Assessment with QR placeholders. Built 2026-04-15 by Bob.
- [x] **Group 5: Building Map v2** — Brand-palette SVG map, KIOSK_LOCATION
  variable, "You Are Here" pulse marker, tap-to-zoom wings, day-aware class
  list per wing, QR placeholder. Built 2026-04-15 by Bob.
- [ ] **Group 6: Wayfinding system** — Photo carousel, data structure, Dan's
  9 photos from March 25 in External Files/. (deferred per Dan 2026-04-15)
- [ ] **Group 7: Device lockdown** — Windows primary (Assigned Access or
  OpenKiosk). iPad/Android secondary.
- [ ] **Group 8: Polish & test** — All devices, both kiosk locations, idle
  reset, QR flow, day detection, responsive testing.

### V2 — Still Open
- **Children's-wing kiosk You Are Here coords** — Dan will provide pixel position.
- **Room class data** — many children's rooms still show "No class" when tapped. Fill in over time.
- **Device lockdown** — Windows Assigned Access. Dan confirming device details.
- **KIOSK_LOCATION** is hardcoded to `'lobby'` near the top of the `<script>`
  block. When Dan deploys on the children's-wing machine, flip that to
  `'childrens-wing'` (the You-Are-Here marker repositions automatically).
- **Cleanup** — unused images (map.png, Building.png, new-here.jpg) can be deleted.
  Build brief + CSV have stale values.

### Key data sources (in External Files/):
- Kiosk Map of Options.docx — Tiri's full feedback (classes, content, structure)
- Building Map Posters 2.pdf — Updated building map from Tiri
- PXL_*.jpg — Dan's 9 wayfinding photos

### Open Questions (DO NOT FORGET — ask Dan about these):
1. **"Different tools" for map wow factor:** What did Tiri mean?
2. **Day detection:** Auto-detect or manual toggle? (Alex recommends auto + hidden override)
3. **Arrow overlays:** Bake into photos or CSS/SVG overlay?
4. **Which device first?** iPad, Android, or Windows?
5. **Windows edition:** Pro/Enterprise or Home on church machines?
6. **External links:** All content in-app with QR for forms? Tiri flagged navigation concern.
7. **Care Groups:** Monthly (not weekly) — how to display?
8. **FriendSpeak:** 3 time slots, 2 rooms — special card layout needed.
9. **Sunday children's classes:** Individual room assignments still needed.
10. **Form URLs:** Need actual URLs for volunteer forms, Small Groups signup, Start Here Card, New Member signup.

---

## STEP 4 — KEY ARCHITECTURE FACTS

### Source
- **Repo:** github.com/wdgrasham/fccc-kiosk
- **Deployed:** https://fccc-kiosk.vercel.app/
- **Vercel project:** prj_VxKSyEj51L9Vh7iO3HAMHn3IMFDR
- **Vercel team:** team_lSA7McVmDKjG622gYUjN8iFa
- **Tech:** Single index.html with inline CSS/JS, SVG building map

### Kiosk locations (2 total)
| Location | Position on Map | Variable Value |
|----------|----------------|----------------|
| Lobby | Near south entrance | `lobby` |
| Children's Wing | A/B wing area | `childrens-wing` |

### Building wings
| Wing | Floor | Color (alpha) | Contents |
|------|-------|---------------|----------|
| Gym Wing | 1st | Green (#D4E8D0) | F-100 through F-112, Chapel, Kitchen |
| A Wing | 1st | Yellow (#FFF9C4) | Rooms 102-122, 132-140 |
| B Wing | 2nd | Blue (#B0D4E8) | Rooms 168-178 |
| C Wing | 1st | Pink (#F8C0D0) | Rooms 202-222 (Elementary) |
| D Wing | 2nd | Purple (#D8B8E8) | Rooms 232-244 (Youth), Conference Room |
| Worship Center | - | Orange (#FFF3E0) | Family Room, Living Room |
| 2nd Floor (above WC) | 2nd | Green (#C8E0C8) | The Studio, East Room |

### Brand colors (from official Branding Style Guide, Feb 2026)
```css
/* Primary */
--deep-teal: #002f3b;    /* dark backgrounds, headers */
--classic-teal: #0a5d67; /* primary dark accents */
--bright-teal: #008c95;  /* buttons, links, interactive */

/* Secondary */
--bright-aqua: #43beac;  /* light accents */
--accent-red: #9d1c30;   /* alerts, emphasis */
--neutral-gray: #808285; /* subtle text, borders */

/* Derived (tints for backgrounds — allowed per guide) */
--teal-light: #E6F7F4;   /* light teal tint for card backgrounds */
```

### Fonts (from official Branding Style Guide)
- **Headlines:** Alfa Slab One (short, high-impact text only)
- **Body/subheadings:** Open Sans (all weights) — NOT Poppins
- **Accent/quotes:** Baskerville Italic (sparingly, scripture/reflective text)

### Bible Classes Navigation Tree
```
Home
  └── Bible Classes
        ├── Sunday Bible Classes
        │     ├── Adult → [class list with rooms and teachers]
        │     └── Children's → [class list with rooms and teachers]
        ├── Wednesday Bible Classes
        │     ├── Adult → [class list with rooms and teachers]
        │     └── Children's → [class list with rooms and teachers]
        └── Small Groups → [link to FCCC signup form]
```

### Wayfinding data structure
```javascript
const wayfinding = {
  'lobby': {
    'ROOM_ID': [
      { image: 'assets/wayfinding/lobby/room-step1.jpg', caption: 'Description' },
      { image: 'assets/wayfinding/lobby/room-step2.jpg', caption: 'Description' }
    ]
  },
  'childrens-wing': {
    'ROOM_ID': [
      { image: 'assets/wayfinding/childrens-wing/room-step1.jpg', caption: 'Description' },
      { image: 'assets/wayfinding/childrens-wing/room-step2.jpg', caption: 'Description' }
    ]
  }
};
```

---

## STEP 5 — FOLDER STRUCTURE

```
FCCC-Kiosk/
├── CLAUDE.md                      # Project rules
├── CLAUDE-STARTUP.md              # This file
├── index.html                     # The kiosk app (single file)
├── specs/
│   ├── KIOSK-REDESIGN-PLAN.md     # V2 redesign plan (Groups 1-5)
│   └── KIOSK-LOCKDOWN-GUIDE.md    # Device lockdown research
└── assets/
    ├── maps/                      # Building map images/SVGs
    └── wayfinding/
        ├── lobby/                 # Photos from lobby kiosk perspective
        └── childrens-wing/        # Photos from children's wing perspective
```

---

## IDENTITY

Read your identity file in this project folder:
- Alex (Cowork): SOUL.md
- Bob (Claude Code): BOB-SOUL.md

After reading, announce yourself and tell a joke. This is the proof of life.

---

## WHO IS DAN

Dan is not a software developer. He's a deep thinker who likes to work through
the full process. Explain technical decisions in plain language. When providing
code or commands, give him step-by-step instructions he can follow. Don't assume
he knows terminal commands, Git workflows, or deployment processes — walk him
through them.

Dan is building this kiosk for his church, First Colony Church of Christ. He's
the one taking the wayfinding photos and coordinating with church staff (the
"she" referenced in notes is likely a church leader providing feedback).

---

## LAST UPDATED

This file was last updated: 2026-04-29
Updated by: Bob (Claude Code)

**Apr 29 (later):** Conference Room marker moved to (1900, 2372). Women's
Bible Group description expanded. Added a generic `series` field to class
data (Families Class now shows "Currently studying: The Fruit of the
Spirit") and a `seriesByMonth` field for auto-rotating titles (International
Fellowship Gospel Project — May/June/July themed). Append numeric keys
to seriesByMonth to add future months; no code change needed.

**Apr 29:** Three content updates — Student Ministry teacher line trimmed
to Nathanial Matis only and a 270px Linktree QR added; "Wednesday Night
Lights" renamed to "Children's Wednesday Night Lights" in 4 places; all
children's room numbers (102, 118, 122, 134, 144, 202–222) hidden from
user-visible text per Dan's security concern. Sunday Children's cards now
show only nicknames/grades; map room headings show "Wing — Nickname"
instead of raw room numbers. Map images (map-1st.png, map-2nd.png) still
contain printed room numbers — Dan to decide separately.

**Apr 22-23:** Massive UI polish session — 42 commits. Standardized card sizing
(420×420 standard, 320×240 compact for 13-card screen). All fonts scaled up.
3-column max grid. Centered layouts everywhere. Info bars centered with QR codes
below at 270px. Teal border stripe on all cards. Children's wing cards (Toddler
Town, Kinder Way, Element Tree) with room assignments. Wing highlight boxes with
exact coords. Volunteer image replaced. Multiple map position tunings (Lobby,
You Are Here). 1st floor map refreshed.

**Apr 15-17:** Built V2 from scratch. Groups 1-5 complete. Visual overhaul
matching firstcolonychurch.org. 69 room circles from CSV. Stacked 1st/2nd floor
maps with blur toggle. Floor-aware legend. Interactive room tap zones. Multi-room
highlighting. Student Ministry card. map-phone.html. All 8 QR URLs.

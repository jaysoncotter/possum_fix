Here's the updated README for the possum_fix repo:

---

# 🐾 Possum — Phonetic Fix Search

**The fastest way to resolve phonetic waypoints, fixes, callsigns, and flight plans in ATC transcription work.**

Possum searches the FAA Coded Instrument Flight Procedures (CIFP) database for fixes and waypoints that sound like what you heard on audio. Type a phonetic approximation, pick your airport, and Possum ranks every matching fix in the area by phonetic similarity — with procedure membership, runway designators, distance, and direction all in one view. Expanded to include airline telephony lookup, military callsign search, FlightAware flight plan retrieval, and full flight path visualization with altitude-coded mapping.

---

## Live Site

**[possumfix.com](https://www.possumfix.com)** — open it, click an airport, type what you heard, hit Search.

---

## What It Does

- **Phonetic fix search** — type what you heard ("gacho", "ramma", "oh lah") and get ranked matches from the actual FAA database
- **Procedure membership** — see exactly which SID, STAR, or approach each fix belongs to, including runway designators (e.g. `ARDIA7.RW35C (SID)`)
- **Fix and procedure search** — search by fix identifier, procedure name, or both simultaneously
- **Multi-sound search** — comma-separate multiple sounds to resolve several unknowns at once
- **Callsign search** — look up airline operator telephonies and military tactical callsigns by phonetic sound using the same scoring algorithms
- **Flight path visualization** — see any flight's filed route plotted on a full-screen map with altitude-coded coloring (ROY G BIV spectrum from red at ground level through violet at 42,000+ ft)
- **Flight plan detail** — view the complete fix-by-fix route with flight level, speed, and geographic location for any flight on any date
- **Live map** — top 25 results plotted on a dark map with color-coded confidence markers
- **28 airport shortcuts** — one-click access to the most common ATC facilities
- **Works offline** — all search logic runs locally in the browser, no server needed

---

## Pages

| Page | URL | What It Does |
|------|-----|-------------|
| **PossumFix** | [possumfix.com](https://www.possumfix.com) | Phonetic fix search, procedure lookup, callsign/telephony search |
| **Playground** | [possumfix.com/playground.html](https://www.possumfix.com/playground.html) | Full-screen flight path map with altitude color coding and collapsible fix list sidebar. Add `?callsign=AAL1487&date=2026-04-05` to load a specific flight. |
| **Playing Possum** | [possumfix.com/playing.html](https://www.possumfix.com/playing.html) | Detailed flight plan view — full route, fix list, altitude/speed data, and date navigation. Requires the Possum Fetcher Chrome extension. |

---

## Files

| File | Description |
|------|-------------|
| `index.html` | Landing page with integrated airport database |
| `beta.html` | The main PossumFix application — phonetic fix search, procedure lookup, callsign/telephony search |
| `playground.html` | Flight path visualization — full-screen Leaflet map with altitude-coded route lines, collapsible slide-over panel with fix-by-fix flight data |
| `playing.html` | Flight plan detail view — fix list with flight levels, speeds, and locations in route order. Fetches data from FlightAware via the Possum Fetcher Chrome extension |
| `cifp_data.json` | Pre-parsed FAA CIFP database — 77,738 fixes, 43,512 with procedure memberships |
| `CNAME` | Custom domain configuration for GitHub Pages (possumfix.com) |
| `README.md` | This file |

---

## Related — The Possum

PossumFix is part of a larger ATC transcription system called **The Possum** — an LLM prompt + Chrome extension that orchestrates PossumFix, FlightAware, and verified data sources into a single transcription workflow.

| Tool | What It Does | Link |
|------|-------------|------|
| **The Possum Prompt** | LLM prompt architecture that parses Global Keys, classifies input, and generates one-click PossumFix links | [github.com/jaysoncotter/The_Possum](https://github.com/jaysoncotter/The_Possum) |
| **Possum Fetcher** | Chrome extension that fetches FlightAware data for Playing Possum and Playground pages | [github.com/jaysoncotter/The_Possum](https://github.com/jaysoncotter/The_Possum) |

---

## Using PossumFix

1. Open [possumfix.com](https://www.possumfix.com) in Chrome or Edge
2. Click an airport button or type an ICAO code
3. Type phonetic sounds in the search bar
4. Hit **Search** or press Enter
5. Results ranked by phonetic similarity with procedure membership, distance, and direction

**For callsign search:** Click the **Callsigns** tab, type an operator name or military callsign, hit Search.

**For flight path visualization:** Visit [possumfix.com/playground.html?callsign=AAL1187&date=2026-02-04](https://www.possumfix.com/playground.html?callsign=AAL1187&date=2026-02-04) — requires Possum Fetcher extension.

---

## Desktop Version

A Python/tkinter desktop GUI version is available in this repo's history and in [The_Possum](https://github.com/jaysoncotter/The_Possum). The web version replaced it for team deployment.

```bash
pip install jellyfish tkintermapview
python possum.py --cifp "C:/path/to/FAACIFP18"
```

---

## Regenerating cifp_data.json

The FAA releases updated CIFP data every 28 days. To update:

```bash
python cifp_to_json.py --cifp "C:/path/to/FAACIFP18"
```

Download the latest CIFP file from:
**https://www.faa.gov/air_traffic/flight_info/aeronav/aero_data/**

---

## How the Phonetic Matching Works

Possum combines five algorithms and scores each fix 0–100:

- **Jaro-Winkler** — string similarity, weighted heavily for short identifiers
- **Soundex** — classic phonetic encoding
- **Metaphone** — more accurate English pronunciation matching
- **Levenshtein distance** — edit distance for near-miss spelling
- **Consonant skeleton** — strips vowels and compares the consonant structure

Results are sorted by score descending, then distance from the airport ascending. Purple markers on the map indicate fixes that belong to a known procedure.

---

## CIFP Data

The FAA Coded Instrument Flight Procedures database is a public domain product of the U.S. Department of Transportation, Federal Aviation Administration. It is not copyrighted under Title 17 U.S.C.

Updated every 28 days. Current cycle: **2602** (effective 19 February 2026)

---

## Built With

- Vanilla HTML/CSS/JavaScript — no frameworks, no build step
- [Leaflet.js](https://leafletjs.com/) — map rendering
- [CartoDB](https://carto.com/) — dark map tiles
- FAA CIFP database — fix and procedure data
- Python + [jellyfish](https://github.com/jamesturk/jellyfish) — desktop version phonetic scoring
- GitHub Pages — hosting

---

Brought to you by *Banana Sandwich Co.* **Snappy · Smart · Badass**

---

**Changes from your current README:**
- Added callsign search, playground, and playing.html to "What It Does"
- Added Pages table showing all three URLs
- Updated Files table to match actual repo contents (index.html, beta.html, playground.html, playing.html, CNAME)
- Added Related section linking to The_Possum repo
- Removed possum.py and cifp_to_json.py from Files table since they're not in the current repo (moved to desktop version section)
- Kept Banana Sandwich Co. branding

Want me to adjust anything or are we good on the READMEs and ready to finalize the resume?

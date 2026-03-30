# 🐾 Possum — Phonetic Fix Search

**The fastest way to resolve phonetic waypoints and fixes in ATC transcription work.**

Possum searches the FAA Coded Instrument Flight Procedures (CIFP) database for fixes and waypoints that sound like what you heard on audio. Type a phonetic approximation, pick your airport, and Possum ranks every matching fix in the area by phonetic similarity — with procedure membership, runway designators, distance, and direction all in one view.

---

## What it does

- **Phonetic search** — type what you heard ("gacho", "ramma", "oh lah") and get ranked matches from the actual FAA database
- **Procedure membership** — see exactly which SID, STAR, or approach each fix belongs to, including runway designators (e.g. `ARDIA7.RW35C (SID)`)
- **Fix and procedure search** — search by fix identifier, procedure name, or both simultaneously
- **Multi-sound search** — comma-separate multiple sounds to resolve several unknowns at once
- **Live map** — top 25 results plotted on a dark map with color-coded confidence markers
- **28 airport shortcuts** — one-click access to the most common ATC facilities
- **Works offline** — all search logic runs locally in the browser, no server needed

---

## Live site

**[possumfix.com](https://possumfix.com)** — open it, click an airport, type what you heard, hit Search.

---

## Files

| File | Description |
|------|-------------|
| `possum.html` | The complete web application — single self-contained file |
| `cifp_data.json` | Pre-parsed FAA CIFP database — 77,738 fixes, 43,512 with procedure memberships |
| `possum.py` | Desktop Python GUI version (requires `pip install jellyfish tkintermapview`) |
| `cifp_to_json.py` | Converter — generates `cifp_data.json` from a raw FAA CIFP file |

---

## Using the web version

1. Open `possum.html` in Chrome or Edge
2. If `cifp_data.json` is in the same folder it loads automatically
3. Otherwise click **📂 CIFP** and select either `cifp_data.json` or the raw `FAACIFP18` file
4. Click an airport button or type an ICAO code
5. Type phonetic sounds in the search bar
6. Hit **Search** or press Enter

---

## Using the desktop version

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

## How the phonetic matching works

Possum combines four algorithms and scores each fix 0–100:

- **Jaro-Winkler** — string similarity, weighted heavily for short identifiers
- **Soundex** — classic phonetic encoding
- **Metaphone** — more accurate English pronunciation matching
- **Levenshtein distance** — edit distance for near-miss spelling
- **Consonant skeleton** — strips vowels and compares the consonant structure

Results are sorted by score descending, then distance from the airport ascending. Purple markers on the map indicate fixes that belong to a known procedure.

---

## CIFP data

The FAA Coded Instrument Flight Procedures database is a public domain product of the U.S. Department of Transportation, Federal Aviation Administration. It is not copyrighted under Title 17 U.S.C.

Updated every 28 days. Current cycle: **2602** (effective 19 February 2026)

---

## Built with

- Vanilla HTML/CSS/JavaScript — no frameworks, no build step
- [Leaflet.js](https://leafletjs.com/) — map rendering
- [CartoDB](https://carto.com/) — dark map tiles
- FAA CIFP database — fix and procedure data
- Python + [jellyfish](https://github.com/jamesturk/jellyfish) — desktop version phonetic scoring

---

Brought to you by *Banana Sandwich Co. *Snappy · Smart · Badass**

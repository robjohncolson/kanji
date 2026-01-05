# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file kanji learning tracker web application. Users select and log kanji they've learned, with progress tracked toward a target date (July 27, 2026 flight to Japan). Features vocabulary review with SRS (Spaced Repetition System), stroke order practice via Hanzi Writer, and data export/import.

## Development

No build system - open `index.html` directly in a browser. Data persists via localStorage.

## Architecture

Single HTML file (`index.html`) containing embedded CSS and JavaScript (~3700 lines total).

### External Dependencies (via CDN)
- Google Fonts: Noto Sans JP, Noto Serif JP
- [Hanzi Writer](https://hanzi-writer.github.io/) - stroke order animation/practice
- qrcode-generator - for sharing progress URLs

### Data Structures

**KANJI_BY_GRADE** (lines ~959-966): Object mapping grade numbers (1-6) to strings of kanji characters. Total: 1,026 jōyō kanji from Japanese elementary school curriculum.

**VOCABULARY** (lines ~997-2700): Array of vocabulary entries with this structure:
```javascript
{ word: "学校", reading: "がっこう", meaning: "school", kanji: ["学", "校"] }
```

**KANJI_READINGS** (line ~2768): Object mapping individual kanji to arrays of readings:
```javascript
{ "日": ["ひ", "にち", "じつ"], ... }
```

### State Management (all localStorage-backed)

| Variable | localStorage Key | Purpose |
|----------|-----------------|---------|
| `learnedKanji` | `learnedKanji` | Set of mastered kanji characters |
| `history` | `kanjiHistory` | Array of learning session entries with timestamps |
| `streakData` | `streakData` | Daily practice streak tracking |
| `srsData` | `srsData` | Spaced repetition intervals per vocabulary item |

### Key Functions

- `renderGradeSections()` / `renderKanjiGrid()` - UI rendering
- `save()` - Persist state to localStorage
- `updateSRS(item, correct)` - Update spaced repetition intervals
- `exportData()` / import handling - JSON backup/restore
- `updateReviewButton()` - Calculate due review items

## Files

- **index.html**: Main application
- **kanji-list.txt**: Reference file with kanji by grade (used when building vocabulary data)

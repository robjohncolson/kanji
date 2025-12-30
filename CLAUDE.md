# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-file kanji learning tracker web application. Users select and log kanji they've learned, with progress tracked toward a target date (July 27, 2026 flight to Japan).

## Architecture

- **kanji-tracker-template.html**: Self-contained HTML/CSS/JS application
  - CSS variables define the theme (Japanese aesthetic with vermillion/gold accents)
  - State stored in localStorage (`learnedKanji` as Set, `kanjiHistory` as array)
  - Kanji organized by Japanese school grade (1-6年生, totaling 1026 characters)
  - The `KANJI_BY_GRADE` object at the top of the `<script>` block needs kanji strings populated from kanji-list.txt

- **kanji-list.txt**: Reference file containing kanji organized by grade level

## Development

No build system - open kanji-tracker-template.html directly in a browser. Data persists via localStorage.

## Key State Variables

- `learnedKanji`: Set of mastered kanji characters
- `selectedKanji`: Set of currently selected (not yet logged) kanji
- `history`: Array of learning session entries with timestamps

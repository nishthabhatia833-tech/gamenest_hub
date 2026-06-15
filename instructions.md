# WD-001: GameNest Hub — Online Gaming Portal

## Project ID: WD-001
**Category:** Web Development
**Subcategory:** Online Gaming Website
**Budget Bracket:** $50–100 USD

---

## Context

GameNest Hub is a fully static, browser-based casual gaming portal where visitors discover, play, and rate lightweight HTML5 mini-games across three categories: Puzzle, Arcade, and Trivia. The platform targets students and office workers seeking five-to-ten minute play sessions with no account creation, no downloads, and no server dependencies. The entire site opens directly from index.html in Chrome, Firefox, Edge, or Safari (latest stable release).

This milestone covers the complete front-end build: five HTML pages, one unified stylesheet, four JavaScript modules, nine embedded open-source games, and all supporting assets. There is no backend, no build pipeline, and no external runtime dependency of any kind. The deliverable is a single ZIP archive that works by double-clicking index.html.

---

## Project Information

| Field | Details |
|---|---|
| Project ID | WD-001 |
| Category | Web Development |
| Project Type | Static Multi-Page Gaming Portal |
| Platform | Browser — Chrome, Firefox, Edge, Safari (latest) |
| Deliverable Type | ZIP archive containing full folder structure |
| Primary Goal | A zero-backend portal where visitors play nine embedded HTML5 games, submit scores to a localStorage leaderboard, and discover games through a filtered catalog |

---

## Main Goal

Build and deliver a complete five-page static gaming portal named GameNest Hub. The site must open from index.html with no server, no npm, and no paid dependency. The three core outcomes are:

1. A working game catalog with real-time category filter and keyword search across nine games.
2. A per-game session leaderboard that reads from and writes to localStorage, persists across page reloads, and displays ranked top-10 entries.
3. A validated game submission form that shows inline field errors and an inline thank-you message on successful submission, with no page reload.

---

## About GameNest Hub

GameNest Hub is an independent community gaming portal with no existing logo, no existing colour palette, and no prior codebase. All visual and technical decisions are defined in this brief. The brand tone is energetic, minimal, and accessible. The tagline is: `Play. Compete. Repeat.`

---

## Requirements

The deliverable is a five-page static website built with HTML5, CSS3, and vanilla JavaScript. Each requirement below is independently testable.

### Page 1 — Homepage (index.html)

1. The page renders a full-width hero section containing the site name in Orbitron font, the tagline "Play. Compete. Repeat." in Inter font, and a single button labelled BROWSE GAMES that navigates to catalog.html.
2. Below the hero, a section labelled FEATURED GAMES displays exactly six game cards drawn from the nine games in the dataset. Each card shows the game title in Orbitron font, a category badge with the correct badge colour, a one-line description, and a PLAY NOW button that navigates to the correct game detail page.
3. The footer appears on every page and contains the text "GameNest Hub -- Community Gaming Portal" on the left and navigation links (Home, Games, Leaderboard, Submit) on the right.
4. The navigation bar appears on every page and contains the logo text "GameNest Hub" in Neon Teal on the left and four navigation links (Home, Games, Leaderboard, Submit) on the right. The active page link is underlined.

### Page 2 — Game Catalog (catalog.html)

5. The page heading reads "All Games" in Orbitron font with a subtitle reading "9 free browser games across Puzzle, Arcade and Trivia" in Inter font.
6. A search input field with placeholder text "Search games..." filters the displayed game cards in real time as the visitor types. Filtering is case-insensitive and matches against both the game title and the one-line description.
7. Four filter buttons labelled All, Puzzle, Arcade, and Trivia are displayed below the search field. Clicking a filter button shows only the cards matching that category. The active filter button is styled with the Neon Teal background colour. The All button is active by default on page load.
8. The filter and search work together: if Puzzle is selected and the visitor types into the search field, only Puzzle games matching the search text are shown.
9. All nine games are rendered as cards in a three-column grid. Each card shows the game title, category badge, one-line description, and a PLAY NOW button.
10. When the search or filter produces zero matches, a message reading "No games found." is displayed in place of the grid.

### Page 3 — Game Detail (game-detail.html)

11. The page reads the query parameter `id` from the URL using URLSearchParams and uses its value to look up the correct game object from the games data array.
12. The game title and category badge are displayed at the top of the page. A back link labelled "Back to Catalog" is placed above the title and navigates to catalog.html.
13. The game is embedded in an iframe. The iframe src is set to the local path `games/{game_id}/index.html` using the id from the URL parameter. The iframe has a minimum height of 480px and a minimum width of 320px.
14. A sidebar panel to the right of the iframe contains three sections: About This Game (one to two sentence description of the game), Controls (listing the keyboard or mouse controls for the game), and Session Leaderboard.
15. The Session Leaderboard section in the sidebar reads from localStorage using the key `gamenest_scores_{game_id}` and displays the top five entries as a ranked list showing rank, player name, and score.
16. Below the Session Leaderboard, a score submission area contains a text input for the player name with placeholder "Your name...", a number input for the score, and a button labelled ADD.
17. Clicking ADD validates that the name input is not empty and the score input contains a positive integer. If either validation fails, no entry is added. If both pass, the entry is pushed to the localStorage array for that game, sorted in descending order by score, trimmed to a maximum of ten entries, saved back to localStorage as a JSON string, and the leaderboard in the sidebar is re-rendered immediately.

### Page 4 — Leaderboard (leaderboard.html)

18. The page heading reads "Leaderboard" in Orbitron font with a subtitle reading "Session scores saved in your browser" in Inter font.
19. A horizontal tab row is rendered with one tab per game, in the same order as the games data array. The first tab is active by default on page load.
20. Clicking a tab reads the localStorage key `gamenest_scores_{game_id}` for the selected game and renders a table with four columns: RANK, PLAYER, SCORE, DATE. Up to ten rows are shown, sorted in descending order by score. If no scores exist for that game, the table body is empty.
21. The rank column displays the rank as #1, #2, #3 and so on. The top-ranked row for the active game is highlighted with a Neon Teal left border and the rank number in Neon Teal.
22. A CLEAR MY SCORES button is displayed below the table. Clicking it calls window.confirm with the message "Clear all scores? This cannot be undone." If the visitor confirms, all localStorage keys beginning with `gamenest_scores_` are deleted and the table is re-rendered to show zero rows.
23. A notice reading "Scores are saved to your browser only and reset when browser data is cleared." is displayed above the CLEAR MY SCORES button.

### Page 5 — Submit a Game (submit.html)

24. The page contains a form with exactly five fields: Game Title (text input), Category (select with options Puzzle, Arcade, Trivia), Game URL (text input), Developer Name (text input), and Description (textarea with a 150-character maximum).
25. A live character counter is displayed below the Description textarea. The counter reads "X / 150" and updates on every keystroke. The counter turns red when the character count exceeds 150.
26. Clicking the submit button without filling all five fields shows an inline error message directly below each empty field. The error message text for each empty field reads "This field is required." No page reload occurs.
27. When all five fields are filled and the description is within 150 characters, clicking the submit button hides the form and displays an inline thank-you message reading "Thank you for your submission! We will review your game soon." No page reload occurs and no backend call is made.

---

## Game Dataset (Public Domain and Open Source)

All nine games below are free to use. Each must be downloaded and stored in its own subfolder under `games/` so the site functions entirely offline.

| # | Title | Category | Licence | Source |
|---|---|---|---|---|
| 1 | 2048 | Puzzle | MIT | github gabrielecirulli/2048 |
| 2 | Hextris | Puzzle | GPL-3 | github Hextris/hextris |
| 3 | Color Flood | Puzzle | MIT | github nicholasgasior/color-flood |
| 4 | Floppy Bird | Arcade | MIT | github nebez/floppybird |
| 5 | Snake Game | Arcade | MIT | github patorjk/snake |
| 6 | Breakout | Arcade | MIT | github strd01/breakout |
| 7 | Trivia Quiz | Trivia | MIT | github joshbuchea/trivia |
| 8 | Open Trivia | Trivia | CC0 | opentdb free public API, no key needed |
| 9 | Trivia Blitz | Trivia | MIT | github guillaumebriday/trivia-app |

Each game subfolder must contain at minimum an index.html file that runs the game when opened in a browser. Folder names must exactly match the id values used in the games data array.

---

## Visual and Technical Specification

### Colour Tokens

All colours are defined as CSS custom properties on the `:root` selector in style.css. No colour value may be used that is not listed here.

| Token Name | Hex | Usage |
|---|---|---|
| Deep Space | #0D0F1A | Page background |
| Card Dark | #1A1D2E | Cards and panels |
| Neon Teal | #00E5CC | Accent colour, buttons, active states |
| Soft White | #E8EAF0 | Body text |
| Muted Grey | #6B7280 | Secondary text, subtitles |
| Purple Badge | #7C3AED | Puzzle category badge background |
| Orange Badge | #EA580C | Arcade category badge background |
| Blue Badge | #2563EB | Trivia category badge background |

### Typography

| Usage | Font | Notes |
|---|---|---|
| Display / Headings | Orbitron | H1, H2, logo text, game titles only |
| Body | Inter | All paragraphs, labels, buttons, inputs |
| Minimum body size | 15px | Line-height 1.6 |

Both fonts are loaded from Google Fonts. No other typefaces are permitted.

### Layout Rules

- Maximum content width is 1200px, centred using `margin: 0 auto`.
- The game catalog grid uses three columns on screens wider than 1024px, two columns between 640px and 1024px, and one column below 640px.
- Game cards have a hover state that applies `transform: translateY(-4px)` and a Neon Teal box-shadow.
- Responsive breakpoints are 640px (mobile) and 1024px (tablet).

---

## Technical Requirements

- Language: HTML5, CSS3, vanilla JavaScript (ES6+).
- No CSS framework. Bootstrap, Tailwind, Bulma, or any third-party stylesheet is not allowed.
- No JavaScript framework or library. React, Vue, jQuery, and all similar libraries are not allowed.
- No backend of any kind. Node, PHP, Python, or any server-side technology is not allowed.
- No paid APIs. No API keys. No authentication.
- No npm, no package.json, no build step of any kind.
- No PWA service workers.
- The site must open by launching index.html directly in a browser with no local server.
- All five pages must load with zero errors in the browser developer console.

### Folder Structure

```
gamenest-hub/
  index.html
  catalog.html
  game-detail.html
  leaderboard.html
  submit.html
  css/
    style.css
  js/
    catalog.js
    game-detail.js
    leaderboard.js
    submit.js
  games/
    2048/
      index.html
    hextris/
      index.html
    color-flood/
      index.html
    floppy-bird/
      index.html
    snake/
      index.html
    breakout/
      index.html
    trivia-quiz/
      index.html
    open-trivia/
      index.html
    trivia-blitz/
      index.html
  assets/
    thumbnails/
      2048.png
      hextris.png
      color-flood.png
      floppy-bird.png
      snake.png
      breakout.png
      trivia-quiz.png
      open-trivia.png
      trivia-blitz.png
```

### localStorage Schema

- Key format: `gamenest_scores_{game_id}` where `{game_id}` is the exact string id from the games data array (e.g. `gamenest_scores_2048`).
- Value format: a JSON string representing an array of objects. Each object has three fields: `name` (string), `score` (integer), `date` (ISO 8601 date string).
- On every write: parse the existing array, push the new entry, sort the array in descending order by score, trim to a maximum of ten entries, and save back using JSON.stringify.
- On clear: iterate `Object.keys(localStorage)` and delete every key whose name begins with `gamenest_scores_`.

### Games Data Array

A JavaScript array named `games` must be defined at the top of catalog.js and imported or duplicated in game-detail.js and leaderboard.js. Each object in the array must have exactly these fields:

```
id          — string, lowercase kebab-case, matches the game subfolder name
title       — string, display name of the game
category    — string, one of: "Puzzle", "Arcade", "Trivia"
description — string, one sentence describing the game
controls    — string, one to two sentences describing keyboard or mouse controls
about       — string, one to two sentences about the game's objective
```

### JavaScript Module Responsibilities

**catalog.js**
- Defines the games array.
- Renders all nine game cards into the catalog grid on page load using innerHTML.
- Attaches event listeners to the four filter buttons and the search input.
- Filter and search run on every button click and every keyup event respectively.
- Filter and search combine: the displayed cards must match both the active category filter and the current search text simultaneously.

**game-detail.js**
- Reads the `id` query parameter from `window.location.search` using URLSearchParams.
- Looks up the matching game object from the games array.
- Sets the page title, category badge, about text, and controls text from the matched game object.
- Sets the iframe src to `games/{id}/index.html`.
- Reads the localStorage key for the game, parses the JSON array, sorts by score descending, and renders the top five entries as a ranked list in the sidebar.
- Attaches a click listener to the ADD button that validates inputs, writes to localStorage, and re-renders the sidebar leaderboard.

**leaderboard.js**
- Builds the tab row dynamically from the games array on page load.
- Sets the first tab as active and renders its leaderboard table.
- On each tab click, updates the active tab style and re-renders the table from localStorage.
- Renders up to ten rows in the table: rank (#1, #2 ...), player name, score, and date formatted as "DD Mon YYYY" (e.g. 14 Jun 2026).
- Attaches the CLEAR MY SCORES button listener that calls window.confirm and deletes all matching localStorage keys on confirmation, then re-renders the current tab's table.

**submit.js**
- Attaches a click listener to the submit button.
- On click, reads all five field values.
- For each field that is empty (or exceeds 150 characters for the description), displays an inline error element immediately below that field. The error element must not exist before submission is attempted.
- If all five fields pass validation, hides the form element and displays the thank-you message div. The thank-you div must already exist in the HTML but be hidden using `display: none` before a successful submission.
- Attaches a keyup listener to the description textarea that updates the character counter on every keystroke.

---

## Thumbnail Assets

Each game requires one thumbnail image in the assets/thumbnails/ folder.

- Dimensions: 400px wide by 225px tall (16:9 ratio).
- Format: PNG.
- File name: matches the game id (e.g. 2048.png, floppy-bird.png).
- Content: a representative screenshot or a flat-colour placeholder with the game title text centred. Placeholder thumbnails are acceptable for games where a screenshot cannot be captured.

---

## Scope Boundaries

### DO
- Build all five HTML pages exactly as specified.
- Use only the eight colour tokens defined in this brief.
- Embed all nine games as local subfolders.
- Implement localStorage read and write for scores.
- Ensure the site opens from index.html with zero console errors.
- Ensure the site is responsive at 375px, 768px, and 1280px viewport widths.

### DO NOT
- Use any CSS framework, JavaScript framework, or external library.
- Add user authentication, cloud storage, or any backend.
- Add analytics, advertising integrations, or tracking scripts.
- Add PWA service workers or a manifest file.
- Use any colour, font, or design token not listed in this brief.
- Introduce any npm dependency or build step.
- Rename or restructure the folder layout defined in this brief.

---

## Deliverable Format

Submit one ZIP archive named `gamenest_hub_{your_name}.zip`. The ZIP must contain the full folder structure defined in the Technical Requirements section. The site must open by launching index.html directly in Chrome, Firefox, Edge, or Safari with no build steps, no local server, and no external runtime dependency.

All nine game subfolders must be present inside `games/` even if fewer than nine games are fully playable in the embedded iframe. All nine thumbnail PNG files must be present inside `assets/thumbnails/`.

### File Naming Convention

```
gamenest_hub_{your_name}.zip
```

All internal files and folders must exactly match the paths listed in the folder structure above. No alternate naming is accepted.

---

## Quality Control Checklist

Before submitting, confirm every item below:

1. All five HTML pages open from index.html with zero browser console errors.
2. The catalog filter and search work together: selecting Puzzle and typing "color" shows only Color Flood.
3. At least six of the nine embedded games are playable in the iframe on their detail pages.
4. A score submitted on a game detail page appears on the leaderboard page for that game after a page reload.
5. The submit form shows inline field errors when submitted empty, and shows the thank-you message when submitted with all fields filled.
6. The site layout is readable and not broken at 375px, 768px, and 1280px viewport widths.
7. No Bootstrap, Tailwind, jQuery, React, Vue, or any third-party CSS or JS file is loaded.
8. No package.json, server file, or API key is present in the deliverable.
9. All eight colour tokens from this brief are used. No additional colour values are introduced.
10. Both Orbitron and Inter fonts are used exactly as specified. No other typeface is introduced.
11. All nine game subfolders exist under `games/` with at minimum an index.html inside each.
12. All nine thumbnail PNG files exist at 400px by 225px inside `assets/thumbnails/`.
13. The CLEAR MY SCORES button calls window.confirm before deleting any localStorage data.
14. The description textarea character counter updates on every keystroke and turns red above 150 characters.
15. The code uses 2-space indentation throughout and all functions and variables have descriptive names.

---

## Acceptance Criteria

The delivery passes only if every item below is true:

1. All five pages load with zero console errors in Chrome DevTools.
2. Catalog filter and search combine correctly as described in requirement 8.
3. Scores written on the game detail page persist and appear on the leaderboard page after a reload.
4. The submit form inline validation and inline thank-you both work without a page reload.
5. The site renders without layout breaks at 375px, 768px, and 1280px.
6. No external CSS or JS library of any kind is loaded.
7. No server, no npm, no build step is required to open the site.
8. All nine game folders are present in the correct path.
9. The colour and font specification from this brief is followed without exception.
10. The localStorage key format `gamenest_scores_{game_id}` is used consistently across all three JavaScript modules.

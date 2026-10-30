# Cryptadoodle

Status: prototype, build 0.1.0-p3.24. Test build hosted at froobaloo.com/cryptadoodle/ (not in the hub menu, hidden from search). Not approved for public release.
Part of the Froobaloo game hub (froobaloo.com). Repo: jtoeman/cryptadoodle.

## Concept

A daily cryptogram. Each tile is one letter of a famous quote, shown in code. Each code letter stands for one real letter, and the mapping is shuffled for every puzzle. The mapping never maps a letter to itself.

Players guess the real letter behind a code letter. Every tile with that code letter is revealed when a guess is right. Points depend on how hard a letter is to pin down.

## Rules

- Tap a tile to select its code letter. Type one letter and press Guess or Enter.
- A correct guess reveals every tile with that code letter and scores points.
- A wrong guess costs 1 point.
- A letter already tried for that code letter, or a letter already found, can't be guessed again. It doesn't score or penalize.
- There are no hints.
- A theme line shows the author or subject of the quote. Any puzzle may have one, and it is optional.

## Scoring

- Value of an unrevealed code letter = (number of unrevealed letters left in its word) × (Scrabble tile value of the real letter).
- A letter in several words uses the lowest word value.
- Points are awarded per occurrence. A letter that appears 3 times in the quote scores 3 times its value when guessed.
- Revealing a letter lowers the value of the other letters in its words by one each.
- Tile values: A1 B3 C3 D2 E1 F4 G2 H4 I1 J8 K5 L1 M3 N1 O1 P3 Q10 R1 S1 T1 U1 V4 W4 X8 Y4 Z10.
- Example: a 9-letter word with a Z is worth 9 × 10 = 90 per Z. A 1-letter word with an A is worth 1.
- Values are current values. They appear under each unrevealed tile and recalculate after each correct guess.
- Scoring is a playtest starting point. Values are expected to change after playtesting.

## Solved state

- Shows the score and the max possible score for the puzzle: every guess right, in the best order.
- The quote is shown on completion.

## Letters Used column

- A column to the right of the gameplay area, under a "Letters Used" header at the theme line.
- Shows only letters that can no longer be used:
  - Green: found.
  - Red: tried wrong against every open code letter.
- A single wrong guess does not add a letter.
- Header and column are always visible, even when empty.

## Layout

- Mobile first: 375 to 430 px. No horizontal scroll.
- Words never wrap. Tiles are as large as fits the longest word, up to 40 px, and resize with the window.
- Order: theme, board, code line, guess box, score, last guess, New puzzle.
- Last guess shows the guessed letter as a tile, then the result: "right, +N" or "wrong, −1".
- Footer: build number, JeremyToeman.com, Ko-fi, Froobaloo.

## Quotes

- Prototype set: To be or not to be (Shakespeare, Hamlet); Knowledge is power (Francis Bacon); Where there is a will, there is a way (Proverb); Stay hungry, stay foolish (Whole Earth Catalog).
- Source: the shared Google Sheet (froobaloodb), tab "Cryptadoodle", columns Date, Quote, Theme. A quote belongs to its date. There is no status.
- The game reads the tab in the browser (gviz CSV, as Sourceword does) and uses today's row (New York date) as the daily quote.
- Past puzzles: a list of every quote dated today or earlier, newest first. Future dates are never listed or played.
- ?day=YYYY-MM-DD opens that past puzzle directly.
- If the sheet is unreachable or the tab is missing, the built-in prototype quotes are used.
- Open issue: the whole tab is downloaded to the page, so future rows can be read by anyone who looks at the network response. See the open items.

## Tutorial

- Built in 0.1.0-p3.10 and reworked in 0.1.0-p3.19 and p3.20: interactive guide started from How to play.
- Steps: tap a tile, make a guess, see a reveal, keep going. No answers are given.
- Same rules as a real puzzle. Scores and max possible are shown when solved.

## Open items

- Playtest 0.1.0-p3.9 and tune scoring values.
- Small tiles on narrow phones with long words fall below the 44 px tap target. Decide the layout for this.
- Tutorial: confirm step wording after playtest.
- Tutorial and How to play are one entry point (How to play button). The tutorial runs on the current puzzle.
- Spoiler exposure: the whole sheet tab is public, so future quotes can be read from the network response. Fix: serve only today and past rows from an Apps Script endpoint, as Caseboard does for its reports.
- Sourceword CC BY-SA attribution is unverified. Confirm before any public launch.
- Word list license: the Wordsummit list is unlicensed in its repo and is not planned for use.
- Nothing is public until the owner approves a release.

## Build log

- 0.1.0-p1: first prototype, quotes and scoring rules.
- 0.1.0-p2: single text entry, tap-to-select tiles.
- 0.1.0-p3: alerts, wrong-guess penalty, score above puzzle, letter column, theme line.
- 0.1.0-p3.1 to p3.3: score and alert visibility, Guess button fix, Enter key.
- 0.1.0-p3.4 to p3.5: letter column to the right, feedback as "Last guess", score under entry.
- 0.1.0-p3.6: no repeat guesses, Clear removed, max possible score, Letters Used header.
- 0.1.0-p3.7: divider full height, board centered.
- 0.1.0-p3.8: words never wrap, tiles shrink to fit.
- 0.1.0-p3.9: Letters Used header at theme level, narrow column, no self-mapping.
- 0.1.0-p3.10: interactive tutorial on a short quote.
- 0.1.0-p3.11: reads daily quotes from the shared froobaloodb sheet, with built-in fallback.
- 0.1.0-p3.12: on phones, keeps the selected tile on screen when the keyboard opens.
- 0.1.0-p3.13: on phones, the code line and guess box float directly above the keyboard, inside a blue border.
- 0.1.0-p3.24: no random quote flashes on load. The page waits for the sheet (a loading line shows meanwhile) and falls back to built-in quotes only if the sheet fails.
- 0.1.0-p3.23: Stats (played, solved, current and best streak, best score) kept on the device. Share result after a solve, with the score and link but no quote.
- 0.1.0-p3.22: first-time visitors get the tutorial automatically. Done or How to play turns it off, and it stays off on return visits (stored on the device).
- 0.1.0-p3.21: connected to the shared sheet (Cryptadoodle tab). Dates without a year (10/20) get the nearest year to today.
- 0.1.0-p3.20: the tutorial works along with today's puzzle (no separate quote, no Back button). How to play toggles it on and off.
- 0.1.0-p3.19: interactive tutorial. Waits for taps and guesses, highlights tiles that share a code, explains scoring in steps, and shows the Letters Used explanation after the first wrong guess. Same-code tiles are highlighted in the real game too.
- 0.1.0-p3.18: tutorial steps advance on their action or on Next, so they can't get stuck.
- 0.1.0-p3.17: How to play is a separate round; today's progress is kept and restored. Tutorial opens with a welcome and the incentive. Letters Used is centered above its column.
- 0.1.0-p3.16: archive of past quotes (Past puzzles, ?day=), no status concept, tiles up to 40 px.
- 0.1.0-p3.15: hosted as a hidden test build at froobaloo.com/cryptadoodle/ (noindex, no menu card).
- 0.1.0-p3.14: How to play and Tutorial are one thing. How to play runs the interactive tutorial, with a blue border.

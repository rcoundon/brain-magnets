# Brain Magnets: notes for Claude

Static PWA, no build step, no dependencies. Everything lives in `index.html` (CSS, markup and JS in one file).

## Structure of index.html
- CSS tokens on `:root`, with dark mode under `prefers-color-scheme` and `[data-theme]`. Use tokens, never literal colours.
- Words data: the `RAW` object, one line per word: `word|synonyms|antonyms|example sentence`, keyed by level 1–3.
- Shape puzzles: `genSeries`, `genOdd`, `genAnalogy`, `genFlip`, `genCodes`. Each returns `{type, prompt, stem, opts, correct, explain, hint}` with options as SVG/HTML strings.
  - Figures are drawn by `figF` (main shape, inner shape, dots, corner square) and `figG` (lopsided shapes for flips/turns, transformed by the matrices in `M`).
  - Generators must guarantee exactly one correct answer and five distinct options.
- Maths: kind tables `SEQ`, `CALC`, `FDP`, `WORD`, `MEASURE` (levels in `*_LV`), run by `genMaths`. Each kind returns `{stem or t, ans, wrong, fmt, explain, hint}`; `mathsOpts` keeps the first four wrong values that render differently. Compute answers from the chosen numbers, never hard-code them.
- Progress is stored in localStorage under `wm-progress` (shape `newP()`); best scores under `wm-best-<mode>-<level>`. Don't rename these keys or players lose progress.

## Rules
- The user is a 10-year-old in the UK: British spelling, plain friendly language.
- After changing any file, bump `VERSION` in `sw.js`.
- Test generators (shapes and maths) by stress-running them (e.g. 400 puzzles per type and level) and checking `opts.length === 5`, unique options, and a valid `correct` index.

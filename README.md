# Brain Magnets

Word puzzles and non-verbal reasoning puzzles for a 10-year-old.

- **Words:** synonym and antonym games across three levels (60 headwords).
- **Shapes:** 11+ style non-verbal reasoning (what comes next, odd one out, analogies, flip & turn, codes), generated on the fly.
- Progress (day streak, answer streak, words mastered, puzzles solved) is saved in the browser's localStorage.
- Installable as an app and works offline.

## Run locally

It's a static site with no build step:

```sh
npx serve .
```

## Deploy

Netlify publishes the repository root (see `netlify.toml`). Pushing to `main` deploys.

When you change any file, bump `VERSION` in `sw.js` (e.g. `wm-v2` → `wm-v3`) so installed copies pick up the update.

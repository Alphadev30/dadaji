# Dadaji Ki Sawaari

A checkpoint racer that trains financial awareness and cyber safety.
Prototype for the CDSL Reimagine Ideathon 2026.

A 92-year-old rides a highway chased by nine scammers. Every ten seconds a
checkpoint spans the whole road: three seconds to read, ten to answer, and you
answer by steering into one of two banners. Three wrong answers and he is off
the bike.

## Run it

It is a static site. No build step, no dependencies.

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

**Do not open `index.html` directly with a double-click.** On `file://` the
browser blocks `fetch()`, so `assets/sprites.json` never loads and the game
silently falls back to its placeholder stick-figure sprites. It will look
broken and you will not be told why. Always serve it over HTTP.

## Deploy to GitHub Pages

```bash
git init -b main
git add .
git commit -m "Dadaji Ki Sawaari prototype"
git remote add origin https://github.com/<you>/dadaji-ki-sawaari.git
git push -u origin main
```

Then: repo **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)`**.
Live in about a minute at `https://<you>.github.io/dadaji-ki-sawaari/`.

The repo must be **public** for Pages on a free account.

## Files

| Path | What it is |
|---|---|
| `index.html` | The whole game. Engine, question bank, learning deck, UI. |
| `assets/sprites.png` | Built atlas, 22 frames, background keyed out |
| `assets/sprites.json` | Frame rectangles and per-frame scale |
| `assets/sprites_*.png` | Original concept sheets, kept as source art |
| `assets/README.md` | How to replace the art |

## Tuning

Numbers worth knowing, all near the top of the script in `index.html`:

| Constant | Does |
|---|---|
| `LIVES` | wrong answers before the run ends |
| `GATE_GAP` | seconds between checkpoints |
| `READ_T` / `ANS_T` | read grace, then answer clock |
| `CENTRIFUGAL` | how hard a corner pulls you wide |
| `STRAIGHT_FIX` | counter-rotation for the three-quarter-view art |
| `const S = [...]` in `buildTrack()` | the track. Hill deltas **must sum to zero** or the loop seam is a cliff |

Question bank is the `BANK` array. Learning deck is `SLIDES`. Roadside signage
is `BOARDS`, `MILES` and `TOWNS`.

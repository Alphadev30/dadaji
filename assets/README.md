# Sprite assets — Dadaji Ki Sawaari

The game ships with every sprite drawn in code (`buildSprites()` in the HTML).
Those are placeholders. Drop a sheet in here and it takes over at runtime.

## How to add art

1. Export one PNG atlas as `assets/sprites.png` (transparent background).
2. Copy `sprites.json.example` to `sprites.json` and correct the frame rects.
3. Tell Claude the files are in — republishing has to include them, because
   the published page can only load files published alongside it.

If `sprites.json` is absent, unreadable, or a key is missing, that sprite
silently falls back to the drawn placeholder. The game never breaks on bad art.

## Frames the engine looks for

| key | what | notes |
|---|---|---|
| `dada` | dadaji riding straight, **rear view** | the hero, seen from behind |
| `dadaL` | leaning left | optional — falls back to `dada` |
| `dadaR` | leaning right | optional — falls back to `dada` |
| `r1` | OTP Chor | rival, rear view |
| `r2` | Fake Broker | rival |
| `r3` | Tip Guru | rival |
| `r4` | Digital Arrest | rival |
| `r5` | Refund Bhai | rival |
| `palm` | roadside palm | |
| `tower` | cell tower | |
| `milestone` | highway milestone | |
| `dhaba` | roadside dhaba | |
| `hoarding` | billboard | good place for an in-world CDSL/SEBI awareness message |

Unlisted keys in the JSON are ignored. Extra scenery needs a code change too
(`kinds` array in `buildTrack()`), so tell Claude rather than only adding art.

## Rules the engine imposes

- **Rear view, not side view.** This is an OutRun-style projection: you are
  looking up the road, so every bike is seen from behind. A side-on Road Rash
  sprite will look wrong.
- **Anchored bottom-centre.** The sprite's bottom edge sits on the road
  surface and its horizontal centre is the bike's position. Leave no empty
  padding below the wheels, or the bike floats.
- **Size comes from frame width.** 80px wide renders as one bike. Double the
  width, double its size on the road. Use `"scale"` per frame to tune without
  re-exporting — `"scale": 1.4` makes it 40% bigger.
- **No fixed sheet size.** Frames can sit anywhere in the atlas; only the
  rects in the JSON matter. Keep the PNG under ~2 MB.
- **One frame per key.** The engine does not animate sprites yet — no walk
  cycles or spinning wheels. Wheel rotation would need an animation field
  added to the loader.

## What is NOT a sprite

- The road, rumble strips and lane markings — drawn as projected polygons.
- The sky, sunset, sun and skyline — a gradient plus rectangles.
- The checkpoint gate — drawn procedurally because it has to stretch to the
  exact projected road width at any distance. A banner texture could be
  layered on top of it later.

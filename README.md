# Worldsmith

Browser-based game-development learning app. The learner writes code, sees a live 3D scene, and an AI coach reads the code and gives feedback. No install, no GPU needed on the learner's side.

## Run

```
npm install
python build.py
python -m http.server 8765 --directory dist
```

Open http://localhost:8765/test.html

`src.html` is the whole app (HTML + CSS + JS). `build.py` inlines three.js and CodeMirror into `dist/`.

## How it works

- User code runs inside a Web Worker (`workerBody` in `src.html`). It can only call the scene API (`ground, tree, rock, house, sun, fog, random`) and returns plain command objects. Endless loops are killed after 1.5 s.
- The main thread validates the commands, builds the three.js scene, then `analyse()` + each mission's `goals / miss / pass` produce the coach feedback.
- Missions live in the `MISSIONS` array. Texts are bilingual (TR/EN).
- Progress and language persist in `localStorage` (`worldsmith.v1`).

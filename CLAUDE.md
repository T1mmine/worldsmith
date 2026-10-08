# Worldsmith: project brief for Claude Code

## What this is
A browser-based game-development learning app, built for the Starnest Academy AI Hackathon 2026 (48 hours, team "Deviltrigger", 3 people, track: **AI Gaming**).

Problem: many people want to get into game development but cannot afford the hardware and engine setup. Worldsmith runs in the browser, needs no powerful computer, teaches by coding along learning paths, and an AI coach reads the learner's code and gives feedback.

Inspiration: *The Farmer Was Replaced*. The learner programs a bot, progress unlocks new commands, and the score is efficiency. Keep it simple: paths, one topic at a time.

Longer-term business ideas (pitch only, do not build): sell as a training set, paid showcase deals with engine/tool companies, community asset marketplace with a commission.

## Judging rubric (design every decision against this)
- 25 value for the user: a specific user and problem, a clear outcome
- 30 prototype and use of AI: a working core scenario, and what the AI actually contributes
- 20 quality testing: tests, examples of failures, comparison with the current approach
- 15 feasibility: data needs, running cost, a clear next step
- 10 originality

Track text (AI Gaming): "Change how a game is played, made or operated, and show the scenario running. A trailer and a slide deck are not a prototype." Relevant examples: procedural content that stays playable, not merely varied; a studio pipeline task cut from a day to an hour.

## Current state
`src.html` is a working single-page demo: live three.js scene on top, CodeMirror editor below, mission card and coach on the right, 4 missions (first tree, loop forest, sunset, own village), TR/EN. User code runs in a Web Worker. See README.md.

**The coach is rule-based, not an LLM.** That scores poorly on "what AI actually contributes", so this is the main gap.

## Next steps, in priority order
1. **LLM coach through a small backend** (Python). Send code + scene summary + mission goals, return a hint that explains what is missing without giving the full answer. Put the model behind one adapter file so Gemini and Claude can be swapped. Cache responses and fall back to the rule-based coach if the API fails or the quota runs out. Gemini free-tier inputs may be used by Google to improve its products, so never send personal data. API keys stay on the server, never in the page.
2. **Solver-verified challenge generation.** The LLM proposes a new challenge (goal + parameters); a reference solver runs it in the same worker sandbox and the challenge is only shown if it is solvable. This is the "procedural content that stays playable" story.
3. **Farmer-style bot missions.** A bot the learner programs (`move`, `plant`, `build`...) with an efficiency score (steps taken) and commands that unlock as missions are completed.
4. **Evaluation harness** (20 points): about 30 deliberately wrong submissions with known problems; measure whether the LLM hint is correct and does not leak the full solution; compare against the static hints. Also log what fraction of generated challenges pass the solver versus raw LLM output, and time-to-first-working-scene for a few real testers versus following a text tutorial. Report only measured numbers.
5. Polish for the demo: a recorded fallback video, no endless spinners, specific error messages.

## Scope rules
- One learning path only ("environment design"), done well. No marketplace, accounts, payments, or real Unity/Unreal embedding (not possible in a browser).
- "AI modelling" means the AI writes or edits scene code that builds objects from primitives. It does not generate neural 3D meshes.
- Hackathon Terms ask to list every model, library, dataset, template and AI assistant used. Keep `ATTRIBUTIONS` up to date: three.js (MIT), CodeMirror 5 (MIT), the LLM(s) used, Claude Code / Gemini as assistants.

## The owner's standing quality checklist (apply to every UI change)
Meaningful empty states; a deliberate, non-uniform palette; dark mode fully styled; touch targets large enough; nothing under the notch or safe area; smooth transitions; specific error messages (never "a problem occurred"); no stuck spinners; the keyboard must not cover inputs; back navigation works; no placeholder text; multi-language (currently TR/EN); confirmation before destructive actions; permissions explained and requested in context. **Test everything before calling it done.**

## Working notes
- Run: `npm install`, `python build.py`, serve `dist/` and open `test.html`.
- After code changes, test in a real browser (Playwright with Chromium works headlessly; WebGL needs `--use-gl=swiftshader --enable-unsafe-swiftshader`).

# Workout Stopwatch

A mobile-first interval timer for gym workouts. Build a custom exercise list, set your work and rest times, and let voice countdowns guide you through every rep.

**[Live Demo](https://ryanbleh.github.io/workout-stopwatch)**

---

## Features

### Exercise List
- Add up to 20 exercises in any order
- Rename, reorder with ↑ ↓ arrows, or delete individual exercises
- The active exercise highlights in the list as the timer runs and scrolls into view automatically

### Saved Workouts
- Save any exercise list + timing settings under a name
- Switch between workouts instantly from the dropdown
- Update an existing workout or fork it under a new name by changing the name on save
- Delete workouts you no longer need
- Everything persists in `localStorage` — workouts survive closing the browser

### Timer
- **Get Ready** countdown (5s) before the first exercise
- **Work** and **Rest** phases with a circular progress ring
- **Circuits** — repeat the full exercise list N times with a configurable rest between circuits
- Skip to the next phase at any time
- Accurate timing using `Date.now()` — stays correct even if the tab is backgrounded briefly

### Voice Countdowns
- Text-to-speech announces every exercise name at the start of each work phase
- During rest: "Rest. Next: [exercise name]"
- Countdown numbers spoken aloud in the last 3, 5, or 10 seconds of each phase (configurable)
- Special calls for the last exercise ("Last one!") and workout completion
- Supplementary audio beeps via Web Audio API for each phase transition and countdown tick
- Toggle voice on/off at any time

### Screen Wake Lock
- Requests a screen wake lock when the timer starts so the phone screen stays on during your workout
- Automatically re-acquires the lock if the OS drops it when switching apps
- Released on pause, reset, and workout complete

---

## Settings

| Setting | Description | Range |
|---|---|---|
| Work Time | Seconds spent on each exercise | 5s – 10m |
| Rest Time | Seconds between exercises | 0s – 2m |
| Circuits | How many times to repeat the full list | 1 – 10 |
| Circuit Rest | Rest between circuits (shown when circuits > 1) | 10s – 5m |
| Voice Countdown | Toggle TTS on or off | — |
| Count from | How many seconds out to start the spoken countdown | 3s / 5s / 10s |

---

## Usage

Open the [live link](https://ryanbleh.github.io/workout-stopwatch) on your phone and add it to your home screen for the best experience.

1. Edit the exercise list or load a saved workout from the dropdown
2. Adjust work/rest times and circuits in the settings panel
3. Hit **Start** — a 5-second "Get Ready" countdown begins
4. The timer announces each exercise name and counts down automatically
5. Tap **Skip →** to jump to the next phase, **Pause** to hold, or **Reset** to start over

> **Note on silent mode:** iOS mutes all web audio (including TTS) when the hardware silent switch is on. Flip it off before your workout to hear voice countdowns.

---

## Tech

Single `index.html` file — no build step, no dependencies.

- **Timer engine** — `requestAnimationFrame` + `Date.now()` for drift-free accuracy
- **Audio** — Web Audio API (oscillator beeps) + Web Speech API (TTS)
- **Wake Lock** — Screen Wake Lock API to prevent screen sleep
- **Storage** — `localStorage` for the active session and all saved workouts
- **Hosting** — GitHub Pages

# LiveScript — Teleprompter Camera

Read your script while looking at the camera. A lightweight, installable web app (PWA):

- 📝 Script editor with autosaved scripts, word count & read-time estimate
- 🎥 Live camera preview with the script scrolling on top
- 🎤 Voice-paced scrolling — the prompter follows your speech
- ⏺ Video recording with countdown, playback review, save & share to camera roll
- 🪞 Mirror mode for glass teleprompter rigs
- 📲 Installable to your home screen, works offline

No build step, no dependencies — a single `index.html` plus a manifest and service worker.

## Run locally

```sh
python3 -m http.server 4173
# open http://localhost:4173
```

Camera and mic require HTTPS or localhost.

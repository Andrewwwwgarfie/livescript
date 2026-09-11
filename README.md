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

## Recording formats and device support

- Choose **16:9 landscape**, **9:16 portrait**, or **Match device orientation** in Settings. Turn the device before recording, then apply settings. Text always wraps into paragraphs and scrolls vertically.
- Choose 720p, 1080p, or 4K, and 30 or 60 fps. These are requests: the status bar reports the actual dimensions and frame rate returned by the camera. If a format is unavailable, the app says so rather than cropping or stretching the video.
- Select an available microphone, switch front/rear cameras, and adjust zoom when the browser exposes it. Settings are locked during countdown and recording.
- Recording uses the original camera MediaStream directly. The script, mirrored preview, and controls are never composited into the recording. Browser encoding still occurs; native Camera app quality, HDR, stabilization, lenses, and phone Camera preferences cannot all be controlled or inherited by a website.
- Open links in Safari or Chrome rather than Messenger/Instagram's embedded browser. Allow both camera and microphone in browser site permissions. **Apply settings / retry camera** retries after permissions change.
- Tap the countdown to cancel. Leaving the foreground stops an active take for review. Keep your device in its starting orientation throughout a take.
- On supported phones, **Share** opens the system share sheet; choose Save Video if offered. **Save Video** downloads the recording, which may go to Files/Downloads rather than Photos.
- Scripts autosave on this device. Voice pacing is for rehearsal; it turns off for recording to avoid competing for the microphone. Browser speech recognition may use an online service.

## Validation

Automated Chromium checks use a synthetic camera and microphone: paragraph layout at 320×568, 393×740, 844×390, and 1024×768; countdown cancellation; record → review → retake; playable video dimensions; script persistence; and uncaught errors. These do not replace physical iOS/Android testing.

Before release on phones, test both orientations, permissions denied/re-enabled, front/rear lenses, a long take, background interruption, audio playback, and Share/Save. Confirm the exported video has no prompt text and matches the capture settings. Long recordings remain in memory until downloaded; available device memory limits take length.

API references: [camera settings](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack/getSettings), [camera capabilities](https://developer.mozilla.org/en-US/docs/Web/API/MediaStreamTrack/getCapabilities), [WebKit recording](https://webkit.org/blog/11353/mediarecorder-api/).

Run the browser checks with the local server running: install `@playwright/test` in a temporary directory, then run `NODE_PATH=/path/to/temp/node_modules node tests/browser.cjs`. Google Chrome must be installed. Screenshots are written to the system temporary directory.

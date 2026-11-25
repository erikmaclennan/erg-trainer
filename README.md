# ERG Trainer

A single-page web app that runs steady ERG workouts on a Wahoo KICKR Core from Chrome on a MacBook. Requirements are in [docs/requirements.md](docs/requirements.md).

## Status

- M1 prototype: connect trainer and heart rate strap, live display, fixed target power, simulator mode.
- M2 workouts: builder with presets saved in the browser, run controls (start, pause, skip, end), ramps, manual offset, auto-pause.
- M3 recording: heart rate cap, one-second ride recording, ride summary, TCX download, lactate log with CSV export, settings.
- M4 Strava: one-time connection, direct upload from the ride summary, duplicate warning.
- M5 polish: ride recovery after a reload, screen wake lock, low cadence (ERG spiral) guard, workout import and export, lactate charts.
- Version 1.1: repeat blocks for intervals, FIT download, guided lactate step test.

## Run

The whole app is `index.html`. Web Bluetooth needs a secure context, so serve it from localhost:

```bash
python3 -m http.server 8765 --bind 127.0.0.1
```

Then open http://localhost:8765 in Chrome or Edge. Add `?sim` to the address to start in simulator mode.

## Strava upload

One-time setup:

1. Create a personal API application at https://www.strava.com/settings/api and set its Authorization Callback Domain to `localhost`.
2. Open the app from http://localhost:8765, go to Settings, and paste the Client ID and Client Secret. They are stored only in the browser's local storage.
3. Press "Connect to Strava" and approve the upload permission.

After a ride, the summary has an "Upload to Strava" button. The ride is sent as a Virtual Ride with the trainer flag set. "Download TCX" stays available as the fallback.

Always open the app at the same address. Saved workouts, rides and the Strava connection belong to that address in that browser.

## Before connecting real devices

- Close the Wahoo app and any other cycling app. The KICKR Core accepts a limited number of Bluetooth connections.
- Free the heart rate strap from the watch or phone if it allows only one connection.
- Garmin HRM 600: switch the strap to its open Bluetooth connection type first. In secure mode the app connects but is refused heart rate data ("GATT operation failed ... while subscribing to 0x2a37").

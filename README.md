# ERG Trainer

A single-page web app that runs steady ERG workouts on a Wahoo KICKR Core from Chrome on a MacBook. It sets the trainer's target power, shows live data, keeps heart rate under a cap, records the ride, and uploads it to Strava.

The whole app is `index.html`. There is no server and no account. Saved workouts, rides, lactate readings, settings and the Strava connection are kept in the browser's local storage.

## Use it

Open https://erg.erikmaclennan.com in Chrome or Edge on the MacBook. Safari and Firefox do not support Web Bluetooth.

Always use the same address. Saved data belongs to that address in that browser.

## Features

- Connect a trainer (Bluetooth FTMS) and a heart rate strap, with automatic reconnect.
- Workout builder with steady, ramp and repeat blocks, presets, and JSON import and export.
- Run controls: start, pause, skip, end, manual power offset, auto-pause.
- Heart rate cap that lowers power in steps while heart rate is over the ceiling, then restores it.
- One-second ride recording, ride summary, TCX and FIT download.
- Direct Strava upload as a Virtual Ride.
- Lactate log with charts and CSV export, and a guided lactate step test.
- Recovery of a ride in progress after an accidental reload.
- Simulator mode for trying everything without hardware. Add `?sim` to the address.

## Before connecting real devices

- Close the Wahoo app and any other cycling app. The KICKR Core accepts a limited number of Bluetooth connections.
- Free the heart rate strap from the watch or phone if it allows only one connection.
- Garmin HRM 600: switch the strap to its open Bluetooth connection type first. In secure mode the app connects but is refused heart rate data ("GATT operation failed ... while subscribing to 0x2a37").

## Strava upload

One-time setup:

1. Create a personal API application at https://www.strava.com/settings/api and set its Authorization Callback Domain to `erg.erikmaclennan.com`.
2. In the app, go to Settings and paste the Client ID and Client Secret. They are stored only in the browser's local storage.
3. Press "Connect to Strava" and approve the upload permission.

After a ride, the summary has an "Upload to Strava" button. "Download TCX" stays available as the fallback.

## Run it locally

Web Bluetooth needs a secure context, so serve the file from localhost:

```bash
python3 -m http.server 8765 --bind 127.0.0.1
```

Then open http://localhost:8765. For Strava from localhost, set the Authorization Callback Domain to `localhost`.

## Hosting

The site is served by GitHub Pages from the `main` branch. The `CNAME` file sets the custom domain.

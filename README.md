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
- Estimated distance and speed from power, for a flat road with no wind. It can be turned off in Settings.
- AI workout builder: describe a workout in plain language and a Claude model builds the blocks for you to review.
- Colour themes, including common editor palettes, with per-colour overrides.
- Floating mini display: a small always-on-top view of power, heart rate, cadence and block time, for watching something else while you ride. Borderless by default; Settings has a window style with buttons.
- Direct Strava upload as a Virtual Ride.
- Lactate log with charts and CSV export, and a guided lactate step test.
- Recovery of a ride in progress after an accidental reload.
- Simulator mode for trying everything without hardware. Start it from Settings, or add `?sim` to the address.

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

## AI workout builder

1. Create an API key at https://console.anthropic.com and give it a spending limit.
2. In the app, go to Settings and paste it under "AI workout builder". It is stored only in the browser's local storage and sent only to Anthropic.
3. On the Workouts tab, describe the ride and press "Build workout". The result opens in the editor so you can check it before saving.

Set your FTP in Settings so zones and percentages are converted to the right watts.

## Run it locally

Web Bluetooth needs a secure context, so serve the file from localhost:

```bash
python3 -m http.server 8765 --bind 127.0.0.1
```

Then open http://localhost:8765. For Strava from localhost, set the Authorization Callback Domain to `localhost`.

## Hosting

The site is served by GitHub Pages from the `main` branch. The `CNAME` file sets the custom domain.

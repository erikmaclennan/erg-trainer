# ERG Trainer

A single-page web app that runs steady ERG workouts on a Wahoo KICKR Core from Chrome on a MacBook. Requirements are in [docs/requirements.md](docs/requirements.md).

## Status

M1 prototype: connect trainer and heart rate strap, live display, fixed target power, simulator mode.

## Run

The whole app is `index.html`. Web Bluetooth needs a secure context, so serve it from localhost:

```bash
python3 -m http.server 8765 --bind 127.0.0.1
```

Then open http://localhost:8765 in Chrome or Edge. Add `?sim` to the address to start in simulator mode.

## Before connecting real devices

- Close the Wahoo app and any other cycling app. The KICKR Core accepts a limited number of Bluetooth connections.
- Free the heart rate strap from the watch or phone if it allows only one connection.

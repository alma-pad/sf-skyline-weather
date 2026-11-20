# sf-skyline-weather

A live, illustrated San Francisco skyline. The sky, clouds and light follow real weather and the real position of the sun and moon: clouds drift slowly with the wind, fog rolls in from the west, and the scene moves through sunrise, day, golden hour, sunset and night.

**Product requirements:** [SF Weather PRD (Google Sheet)](https://docs.google.com/spreadsheets/d/1prN2_OC81xMdon5NjJPNXSOHNuveCDYQRoM4o-UbYQU/edit?gid=0#gid=0). Each requirement has an ID (e.g. `S1`, `C2`), a priority (MVP / P1 / P2) and a status.

## Pages

| File | What it is |
| --- | --- |
| `index.html` | The dashboard: the illustrated skyline scene with the current time and date |
| `stats.html` | Raw data page: every weather, sun and moon value the scene uses (PRD `D1`) |

## Data sources

- **[Open-Meteo](https://open-meteo.com/)**: current weather for SF (lat 37.7749, lon -122.4194), refreshed every 15 minutes. Free, no API key. Units: °F, mph, inches.
- **[SunCalc](https://github.com/mourner/suncalc)**: sun altitude/azimuth, sunrise/sunset, golden hour, twilight, and moon position/phase, computed in the browser.

## Art

Illustrations are drawn in Procreate and exported as transparent PNGs into `assets/`.

- `assets/skyline_rough_sketch.png`: first rough skyline sketch (2732×2048, skyline along the bottom).

## Running it

No build step. Open `index.html` in a browser, or serve the folder:

```
python3 -m http.server 8000
```

then visit http://localhost:8000.

## Status

- [x] Raw data test page (`D1`), weather fetch (`D2`), sun and moon calculations (`D3`)
- [x] Current time on the dashboard (`U1`)
- [ ] Sky gradient, clouds, day/night: see the PRD for the full list

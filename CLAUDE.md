# CLAUDE.md

Context for working on this project. See `README.md` for the overview.

## What this is

A live, illustrated SF skyline dashboard. The skyline art and drifting clouds respond to live weather (Open-Meteo) and the sun/moon position (SunCalc). The owner draws the art in Procreate; code animates and composites it.

The requirements live in a Google Sheet PRD (link in `README.md`). Refer to requirements by their ID (`L1`, `S1`, `C2`, `T1`, …) and respect their priority: build MVP items before P1/P2 unless asked.

## Stack and conventions

- Plain static HTML/CSS/JS. No build step, no framework, no npm. Keep it that way unless the owner asks otherwise.
- External scripts load from cdnjs with a pinned version (SunCalc 1.9.0).
- Location is fixed to San Francisco: lat 37.7749, lon -122.4194, time zone `America/Los_Angeles`. Always format times in that zone.
- Units: °F, mph, inches. Visibility comes back from Open-Meteo in feet when using Fahrenheit.
- Art goes in `assets/` as transparent PNGs.

## Architecture direction (from the PRD)

- **One "sky state" object** drives every visual (time of day, cloud cover by layer, fog, wind, rain). It can be filled from live data or overridden by the debug panel / playground sliders (`T1`, `P1`). Visuals should read only from sky state, never directly from the API.
- **Smooth everything**: ease into new weather values over 1–2 minutes (`W3`); interpolate sky gradients by sun altitude rather than switching day/night (`S1`).
- **Clouds drift very slowly**; scale wind speed way down (`C2`).
- **The scene faces south**: east (Ferry Building) is on the left, west (Sutro Tower, where fog arrives) is on the right. Sun azimuth maps left-to-right (`S4`).
- **Fallback**: if a fetch fails, keep the last known weather; the sky still follows the clock (`D5`).

## Pages

- `index.html`: the dashboard scene.
- `stats.html`: raw data / debug view of all inputs (`D1`). Useful for checking values while building visuals.

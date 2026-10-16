# World Radio

A spinning world globe for the Omarchy bar. Click for a big globe of
every country — hovering a country, city, or town plays live radio from
there.

![World Radio globe popup](preview.png)

## Install

```sh
omarchy plugin add https://github.com/kaibur02/omarchy-world-radio.git --enable
```

## Usage

Click the globe icon in the bar to open or close the world globe.
Press Escape to close it.

- Hover a globe dot, country row, or station row to tune in live radio
  from there (toggleable via the `hover ▶` button; when off, playback
  is click-only).
- Drag the globe to spin it by hand.
- Right-click the bar icon to stop playback, middle-click to open
  radio.garden in a browser.
- `/` focuses search — it matches every station name worldwide from a
  local catalog (~50k stations indexed in memory, refreshed every few
  days and cached under `~/.cache/quickshell/world-radio/`), so results
  are instant and unlimited; it also lists the countries that have
  matches. Clicking a result plays it and selects its country, keeping
  the results; `Enter` plays the top result, `Space` toggles play/stop.
- Country lists come from the same local catalog (click-ranked), not
  just the API's top 30.

## Configure

```sh
omarchy bar move io.github.kaibur02.omarchy-world-radio --after omarchy.weather
omarchy bar set io.github.kaibur02.omarchy-world-radio hoverPlay false
```

## Remove

```sh
omarchy plugin remove io.github.kaibur02.omarchy-world-radio
```

## Details

- Station directory and streams via
  [radio-browser.info](https://www.radio-browser.info) (no API key needed).
- The full working-station catalog (~50k) is indexed in memory for
  instant search; the first run downloads it in the background (~80 MB,
  a minute or two), then a disk snapshot under
  `~/.cache/quickshell/world-radio/` makes every later start instant.
  The snapshot refreshes itself when older than three days.
- Spam is extinguished: a radio's identity is its stream — any URL
  appearing more than once in the directory (global streams registered
  under dozens of countries, duplicate rows) has every copy removed
  from the local catalog, on every load and refresh.
- Fully theme-reactive: every color comes from Omarchy's `Color`/`Style`
  singletons, so theme switches restyle the plugin live.
- No install hooks, no sudo, no background services. Runs entirely
  inside `omarchy-shell` as an unsandboxed QML plugin with standard user
  permissions.

## Files

| File            | What                          |
|-----------------|-------------------------------|
| `manifest.json` | Omarchy plugin manifest       |
| `Widget.qml`    | Bar widget + globe popup      |
| `Globe.qml`     | Canvas orthographic globe     |
| `Model.js`      | Country coordinates + API helpers |
| `preview.png`   | Marketplace preview screenshot |

## IPC

```sh
omarchy-shell io.github.kaibur02.omarchy-world-radio toggle   # open/close the globe
omarchy-shell io.github.kaibur02.omarchy-world-radio stop     # stop playback
omarchy-shell io.github.kaibur02.omarchy-world-radio status   # JSON state
```

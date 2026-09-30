# One Tile Village

A cozy isometric farming-village game that runs in the browser. It is based on the "0 days to 1000 days" idea: you start with a single grass block and one small hooded farmer, and grow it into a village over 1000 in-game days.

The game itself is one file (`www/index.html`) with no build step and no image assets. All the pixel art is drawn from code at startup, and the two pixel fonts are bundled in `www/fonts`, so it works offline.

It is wrapped as a phone app with [Capacitor](https://capacitorjs.com), so the same code ships as an Android app and an iOS app. Progress saves automatically on the device.

## Play in a browser

Open `www/index.html` directly, or run `npm install && npm run serve` and visit http://localhost:8080.

## Build the phone app

You need Node 18+ and `npm install` once.

**Android** (Android Studio, or the Android SDK plus JDK 17+):

```sh
npm run android        # syncs the game into android/ and opens Android Studio
```

Then press Run for a device or emulator, or use *Build > Build Bundle(s) / APK(s)*. From a terminal, `cd android && ./gradlew assembleDebug` writes `app/build/outputs/apk/debug/app-debug.apk`.

**iOS** (a Mac with Xcode):

```sh
npm run ios            # syncs the game into ios/ and opens Xcode
```

Pick a team under *Signing & Capabilities*, then Run.

After editing `www/index.html`, run `npm run sync` to copy it into both native projects. The app id is `com.ofek.onetilevillage` (change it in `capacitor.config.json` before publishing). Icons and splash screens come from `assets/` via `npx capacitor-assets generate`.

Note: I could not compile the Android or iOS builds in the sandbox where this was written (no Android SDK or Xcode), so the first native build on your machine is the first real test.

## How it works

- **Land** extends your island one tile at a time. Each tile costs a little more than the last.
- **Wheat** ripens in 4 days and gives 3 wheat. Click ripe wheat to harvest it, or let villagers do it. Villagers replant for 1 coin.
- **Sell** wheat with the Sell all button (70% price), or click a **Shop**, **Stall** or **Cart** for full price. Those buildings also sell automatically every morning.
- **Windmill** grinds wheat into flour, which sells for much more.
- **House** brings a new villager who harvests for you.
- **Well** speeds up wheat within 2 tiles. **Trees, paths and buildings** add charm, and charm raises every sale price (up to double).
- Tools unlock as your land grows. Seasons change every 30 days and there is a day and night cycle.
- Reach day 1000 to finish. You can keep playing afterwards.

## Controls

| Input | Action |
| --- | --- |
| Left click / drag | Use the selected tool (drag to plant or build in a line) |
| Hand tool drag, or right-drag | Pan the camera |
| Mouse wheel, `+` / `-` | Zoom |
| `W A S D` / arrow keys | Move the camera |
| `1`-`9`, `0`, `C`, `X` | Pick a tool |
| `Space` | Pause |
| `M` | Mute |

The 1x / 3x / 10x buttons change game speed. A full 1000 days takes about 10 minutes at 10x.

## Developer handle

`window.OTV` exposes the game state for poking around in the console, for example `OTV.demo()` builds a small finished village.

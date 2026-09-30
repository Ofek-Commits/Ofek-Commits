# One Tile Kingdom

A fantasy-medieval village builder that runs in the browser. It is based on the "0 days to 1000 days" idea: you start with a single grass block and one crowned, hooded lord or lady, raise your own house, and grow it into a kingdom over 1000 in-game days.

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

- **Your home** is free and you get one. Pick the Home tool and click your grass. Click the house later to name your village, choose your house colours and upgrade it: Cottage, Manor, Keep, then Castle. Each level adds charm and a retainer. The Keep and Castle add knights.
- **Your village** starts as a Hamlet and grows into a Village, Town, City and finally a Kingdom as you claim land. Its name and rank show in the top left.
- **Land** extends your island one tile at a time. Each tile costs a little more than the last.
- **Wheat** ripens in 4 days. Click ripe wheat to harvest it, or let villagers do it. Villagers replant for 1 coin.
- **Selling:** use the Sell all button (70% price), or click a **Shop**, **Stall**, **Tavern** or **Cart** for full price. Those buildings also sell automatically every morning.
- **Windmill** grinds wheat into flour, which sells for much more.
- **Cottage** brings a peasant family who harvest for you. **Well** speeds up nearby wheat.
- **Smithy** adds wheat to every harvest (up to +2). **Chapel** (needs a Manor) adds a lot of charm. **Wizard tower** (needs a Keep) speeds up wheat within 3 tiles by 75%.
- **Charm** from trees, paths and buildings raises every sale price, up to double.
- Seasons change every 30 days, there is a day and night cycle, and a dragon sometimes flies over. Click it for a treasure.
- Reach day 1000 to finish. You can keep playing afterwards.

## Controls

| Input | Action |
| --- | --- |
| Left click / drag | Use the selected tool (drag to plant or build in a line) |
| Hand tool drag, or right-drag | Pan the camera |
| Mouse wheel, `+` / `-` | Zoom |
| `W A S D` / arrow keys | Move the camera |
| `1`-`9`, `0`, `H`, `C`, `T`, `B`, `V`, `G`, `X` | Pick a tool (Home, Cart, Tavern, smithy (B), chapel (V), wizard (G), Clear) |
| `Space` | Pause |
| `M` | Mute |

The 1x / 3x / 10x buttons change game speed. A full 1000 days takes about 10 minutes at 10x.

## Developer handle

`window.OTV` exposes the game state for poking around in the console, for example `OTV.demo()` builds a small finished village.

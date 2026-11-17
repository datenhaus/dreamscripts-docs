# Dream Loading

A loading screen for FiveM servers. Your logo is built from 1-3 letters, your colour comes from one line in the config, and the progress bar follows the real loading progress of the game. No image editing needed.

> Built with AI assistance, tested on our live roleplay server DreamRP (ESX Legacy). Other frameworks are marked as beta where they apply. Version 1.0.0 (from `fxmanifest.lua`). Resource folder: `dream_loading`.

## Features

- Progress bar with percent and the current stage, with a fallback so the screen never looks frozen
- Logo badge from 1-3 letters, server name and tagline
- Tabs for news, rules and team (up to 4 tabs, up to 20 entries each)
- Rotating tips under the progress bar, info line for Discord and website (plain text)
- Built-in animated background, or your own picture slideshow, or your own video
- Optional music with volume slider and mute button, the volume is remembered
- Keyboard: Space music on / off, arrow up / down volume, arrow left / right switch tabs
- Stays open until the player has spawned, then fades out, a timeout makes sure nobody gets stuck
- Primary colour and text colour in the config
- No database, no web requests, no commands, no server events

Not included: background pictures, videos and music. You add your own.

## Requirements

- None. No `dependencies` in `fxmanifest.lua`.
- Works without any framework. Optional spawn events of ESX Legacy and QBCore are in the default close list.

## Installation

1. Put the folder `dream_loading` into your `resources` folder.
2. Add `ensure dream_loading` to your `server.cfg`.
3. Remove or stop any other loading screen resource. Only one can be active.
4. Edit `html/config.js` (name, colours, logo letters, tips, tabs, links).
5. Restart the server.

Preview without a server: open `html/index.html` with a double click. The progress bar runs as a demo.

## Configuration

Editable files (stay open under Asset Escrow): `html/config.js`, `html/locales.js`, `config.lua`, `html/assets/`.

Page options in `html/config.js`:

| Option | Default | Meaning |
| --- | --- | --- |
| `locale` | `'en'` | `'en'` or `'de'` |
| `theme.primary` / `theme.text` | `#F5C400` / `#F4F2EA` | Colours |
| `theme.logoText` | `'DS'` | 1-3 letters |
| `theme.serverName` / `theme.tagline` | `'Your Server'` / sample line | Headline and line below |
| `background.video` / `images` | empty | File names in `html/assets` |
| `background.seconds` / `dim` | `9` / `0.55` | Seconds per image, darkening |
| `music.file` / `volume` / `remember` | empty / `0.25` / `true` | Music |
| `tips`, `tipSeconds` | sample tips, `6` | Tips |
| `tabs`, `links`, `showKeys`, `fallbackAfterSeconds` | sample content | Tabs, info line, key hint, fallback |

Closing behaviour in `config.lua`:

| Option | Default | Meaning |
| --- | --- | --- |
| `Config.Debug` | `false` | Print the reason for closing to the F8 console |
| `Config.Shutdown.events` | `playerSpawned`, `esx:playerLoaded`, `QBCore:Client:OnPlayerLoaded` | Events that close the screen |
| `Config.Shutdown.delayMs` / `fadeMs` | `1500` / `800` | Wait and fade time |
| `Config.Shutdown.timeoutSeconds` | `45` | Safety net |
| `Config.Shutdown.closeGameScreen` | `true` | Also close the built-in GTA loading screen |

Own media: copy files into `html/assets`, enter the file names, restart the server. Video `.webm` or `.mp4` (`.webm` recommended), pictures `.jpg`, `.png`, `.webp`, music `.ogg` or `.mp3`. Only use media you have the rights for.

## Commands and keys

No commands. Keys while the loading screen is open: Space (music), arrow up / down (volume), arrow left / right (tabs).

## Exports and events

Client side:

- `exports['dream_loading']:Shutdown()` closes the loading screen now, returns `true` if it was still open
- `exports['dream_loading']:IsOpen()` is `true` while the script has not started closing it

## Localization

English (default) and German via `locale` in `html/config.js`. Fixed labels are in `html/locales.js`. All config texts are shown as plain text, HTML is not interpreted.

## Performance

Resmon values are **estimated from the code, set low on purpose** (not measured on every server setup): idle roughly 0.00-0.01 ms. Values rise briefly while the interface is open or while the script handles a request. Please check `resmon` on your own server.

## FAQ and troubleshooting

**The loading screen stays long after the game has loaded.** None of the events in `Config.Shutdown.events` arrived, so the timeout closed it. Set `Config.Debug = true`, read the F8 console and add your framework's spawn event.

**It covers my character selection.** Add the "selection opened" event to `Config.Shutdown.events` or call `exports['dream_loading']:Shutdown()` from it.

**I want the old behaviour (close as soon as the game data is loaded).** Delete the line `loadscreen_manual_shutdown 'yes'` in `fxmanifest.lua`.

**Music or video does not work.** Check the file name (upper and lower case matter on Linux), that the file is in `html/assets`, and restart the server. Use `.ogg` and `.webm`.

**The page shows "Your Server" after my edit.** There is a typing mistake in `html/config.js`, usually a missing comma or quote. Open `html/index.html`, press F12 and read the Console tab.

**Can players click the Discord link?** No, a loading screen cannot open web pages. The info line is plain text.

## Support

- Support Discord: https://discord.gg/XhHQkkXkFW
- Store: https://dreamscripts.tebex.store
- All documentation: [DreamScripts Docs](../README.md)

## Changelog (short)

- 1.0.0 (2026-11-13): First release. Progress bar with stages, tabs, tips, optional background and music, manual shutdown after spawn with fade out.

Full changelog: `CHANGELOG.md` inside the resource.

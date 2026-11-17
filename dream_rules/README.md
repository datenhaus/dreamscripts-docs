# Dream Rules

A welcome window with your server rules. New players see the rules by category, scroll to the end, then accept or decline. The acceptance is saved per player without a database. Raise one number and everybody is asked again.

> Built with AI assistance, tested on our live roleplay server DreamRP (ESX Legacy). Other frameworks are marked as beta where they apply. Version 1.1.0 (from `fxmanifest.lua`). Resource folder: `dream_rules`.

## Features

- Rules by category with navigation, numbering (1.1, 1.2, ...) and a reading progress bar
- "Accept" becomes active after scrolling to the end (fallback unlocks it after 45 seconds so nobody gets stuck)
- Minimum reading time, checked on the server
- Decline needs two clicks, then the player is disconnected with your message, or the window stays open (your choice)
- Saved per player identifier in one JSON file inside the resource, no database
- Rules version in the config: raise it and every player accepts again
- `/rules` opens the rules for reading at any time
- Staff commands `/rulescheck` and `/rulesreset`
- Permission by ESX group or ACE
- Optional Discord log of every acceptance (webhook only in `server_config.lua`)
- Exports and a server event for your own scripts

## Requirements

- None. No hard dependency in `fxmanifest.lua`.
- Optional: `es_extended` (ESX Legacy). With ESX, start this resource after `es_extended`. ESX is only used for the admin permission.

## Installation

1. Put the folder `dream_rules` into your `resources` folder. Do not rename it.
2. Add `ensure dream_rules` to your `server.cfg`. With ESX, put it after `es_extended`.
3. Edit `config.lua`: server name, colour, logo letters and your rules in `Config.Categories`.
4. Restart the server.

Without ESX, give your admins the permission in `server.cfg`:

```
add_ace group.admin dream_rules.admin allow
```

Preview without a server: open `html/index.html` with a double click (sample rules).

## Configuration

Main file: `config.lua`. Texts: `locales.lua`. Server-only: `server_config.lua` (`Webhook`, `BotName`).

| Option | Default | Meaning |
| --- | --- | --- |
| `Config.Locale` | `'en'` | `'en'` or `'de'` |
| `Config.RulesVersion` | `1` | Raise it to ask everybody again |
| `Config.Theme` | gold accent | `primary`, `logoText`, `serverName` |
| `Config.Categories` | sample rules | Up to 20 categories, up to 50 rules each |
| `Config.RequireScroll` | `true` | Accept only after scrolling to the end |
| `Config.MinReadSeconds` | `5` | Minimum time before "Accept" (0 - 300), checked on the server |
| `Config.OpenDelayMs` | `3000` | Wait after spawning before the window opens |
| `Config.ScrollFallbackSeconds` | `45` | Safety net for the scroll requirement |
| `Config.Decline` | `kick = true` | Disconnect on decline, with optional message |
| `Config.Command` | `'rules'` | `''` = no command |
| `Config.CheckCommand` | `'rulescheck'` | Staff lookup, `''` = no command |
| `Config.Admin` | `rulesreset`, groups `admin`, `superadmin`, ACE `dream_rules.admin` | Admin command and permission |
| `Config.SpawnEvents` | `playerSpawned`, `esx:playerLoaded`, `QBCore:Client:OnPlayerLoaded` | Events that open the window |
| `Config.FallbackSeconds` | `60` | Ask anyway after this many seconds if no event arrives |
| `Config.Identifier` | `'license'` | Preferred identifier, never the IP address |
| `Config.Log` | `true` | Print accept, decline, reset to the server console |

Changing the rules: edit `Config.Categories` and raise `Config.RulesVersion` by 1. Fixing only a typo? Leave the number.

Data: `accepted.json` inside the resource folder, created on the first acceptance. Back it up, keep it when updating the script.

## Commands and keys

| Command | Who | Action |
| --- | --- | --- |
| `/rules` | everyone | Opens the rules for reading (the accept window if not accepted yet) |
| `/rulescheck <player id or identifier>` | staff | Shows if and when a player accepted which version |
| `/rulesreset <player id>` | admins, console | The online player has to accept again right away |
| `/rulesreset <identifier>` | admins, console | Deletes the saved acceptance of an offline player |
| `/rulesreset all` | console only | Deletes every saved acceptance |

Command names can be changed in the config.

## Exports and events

Server side:

- `exports['dream_rules']:HasAccepted(source)` returns `true` if the player accepted the current version
- `exports['dream_rules']:Reset(source)` makes the player accept again (returns `false` if offline)
- Event `dream_rules:accepted` with `playerId, identifier, version`, runs every time a player accepts

Client side: `exports['dream_rules']:IsOpen()` is `true` while the window is on screen.

## Localization

English (default) and German via `Config.Locale`. All texts are in `locales.lua`. To add a language, copy the `Locales.en` block, rename it (for example `Locales.fr`), translate it and set `Config.Locale = 'fr'`. Missing texts fall back to English.

## Performance

Resmon values are **estimated from the code, set low on purpose** (not measured on every server setup): idle roughly 0.00-0.01 ms. Values rise briefly while the interface is open or while the script handles a request. Please check `resmon` on your own server.

## FAQ and troubleshooting

**The window does not open for new players.** Check the console for errors of `dream_rules`. If your framework sends none of `Config.SpawnEvents`, it opens after `Config.FallbackSeconds`. Add your framework's spawn event.

**It opens over my character selection.** Remove `playerSpawned` from `Config.SpawnEvents` and keep only the "player loaded" event, or raise `Config.OpenDelayMs`.

**A player cannot click "Accept".** He must scroll to the end. After `Config.ScrollFallbackSeconds` the button becomes active anyway. With `Config.MinReadSeconds` the button shows a countdown.

**I do not want to kick players who decline.** Set `Config.Decline.kick = false`.

**Players have to accept again after every restart.** `accepted.json` could not be written. Check the write permissions of the resource folder.

**Another script already uses `/rules`.** Change `Config.Command`.

## Support

- Support Discord: https://discord.gg/XhHQkkXkFW
- Store: https://dreamscripts.tebex.store
- All documentation: [DreamScripts Docs](../README.md)

## Changelog (short)

- 1.1.0 (2026-11-15): New staff command `/rulescheck`, optional Discord log of every acceptance.
- 1.0.0 (2026-11-13): First release. Rules window, scroll and reading time checks, accept / decline, `accepted.json`, exports.

Full changelog: `CHANGELOG.md` inside the resource.

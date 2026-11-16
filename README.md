# DreamScripts Documentation

Documentation for DreamScripts, FiveM scripts by DreamStudios.

- Store: https://dreamscripts.tebex.store
- Support Discord: https://discord.gg/XhHQkkXkFW

> Built with AI assistance, tested on our live roleplay server DreamRP (ESX Legacy). QBCore, Qbox and standalone support is marked as beta where it exists: tested in simulation, not yet on a live server.

## Scripts

| Script | Version | Frameworks | Required resources | Docs |
| --- | --- | --- | --- | --- |
| Dream Cards | 1.1.1 | ESX Legacy | es_extended, oxmysql | [dream_tcg](./dream_tcg/README.md) |
| Dream Moneywash | 1.1.2 | ESX Legacy | es_extended, oxmysql | [dream_moneywash](./dream_moneywash/README.md) |
| Dream Billing | 1.1.6 | ESX Legacy | es_extended, oxmysql | [dream_billing](./dream_billing/README.md) |
| Dream Elevator | 1.1.2 | ESX Legacy | es_extended, oxmysql | [dream_fahrstuhl](./dream_fahrstuhl/README.md) |
| Dream Scoreboard | 2.3.1 | ESX Legacy; QBCore, Qbox, Standalone (beta) | none | [dream_scoreboard](./dream_scoreboard/README.md) |
| Dream Adminjail | 1.3.2 | ESX Legacy; QBCore, Qbox, Standalone (beta) | oxmysql | [dream_adminjail](./dream_adminjail/README.md) |

## Free script

| Script | Docs |
| --- | --- |
| Dream Notify (free, standalone, ESX / QBCore optional) | [github.com/datenhaus/dream_notify](https://github.com/datenhaus/dream_notify) |

## General notes

- Every script has its own `README.md` with features, requirements, installation, configuration, commands, exports, localization, performance, troubleshooting and changelog.
- All scripts ship in English (default) and German.
- Editable files (`config.lua`, `locales.lua`, `server_config.lua`) stay open when the resource is protected by Cfx.re Asset Escrow.
- Resmon values in the docs are estimates from the code, kept low on purpose. Please measure on your own server.
- Discord webhooks are always entered in server-only files, never in shared configs.

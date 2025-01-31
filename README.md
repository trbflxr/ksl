# KSL

[![Releases](https://img.shields.io/github/v/release/trbflxr/ksl?include_prereleases&label=DOWNLOAD&style=for-the-badge)](https://github.com/trbflxr/ksl/releases)
[![Kino Discord](https://img.shields.io/discord/716264804498538516?label=DISCORD&style=for-the-badge)](https://discord.gg/xvGMEEcEEp)

## About

KSL is an advanced mod loader developed for **Unity mono** games.

Supported platforms:

* Windows x64
* macOS (WIP tested only on Ventura 13.1)

Game and system requirements:

* Unity mono runtime
* Steamworks, currently Facepunch.Steamworks and Steamworks.NET are supported
* Internet connection

> [!NOTE]  
> **Installation** guide can be found [here](https://github.com/trbflxr/ksl/blob/master/doc/guide/install.md).
>
> Learn how to **setup and configure** KSL [here](https://github.com/trbflxr/ksl/blob/master/doc/guide/setup.md).
>
> **Mods / extension** installation guide can be found [here](https://github.com/trbflxr/ksl/blob/master/doc/guide/install_content.md).

## Features

* Well documented [API](https://github.com/trbflxr/ksl/blob/master/doc/api/api.md)
* In-game devtools:
    * [Control panel](https://github.com/trbflxr/ksl/blob/master/doc/guide/dev/control_panel.md) for mods / extensions
    * [Release validation](https://github.com/trbflxr/ksl/blob/master/doc/guide/dev/updater.md#create-and-test-release-archive) tools
* An [auto updater](https://github.com/trbflxr/ksl/blob/master/doc/guide/dev/updater.md) to keep installed mods updated
* In-game expandable [UI](https://github.com/trbflxr/ksl/blob/master/doc/api/ui.md) for mods and extensions
* Mod encryption
* Support for [private mods](https://github.com/trbflxr/ksl/blob/master/doc/guide/dev/control_panel.md#whitelist-management) (steamID-locked)
* KSL [extensions](https://github.com/trbflxr/ksl/blob/master/doc/guide/dev/extensions.md) system
* [Input manager](https://github.com/trbflxr/ksl/blob/master/doc/api/input.md)
* Advanced [config](https://github.com/trbflxr/ksl/blob/master/doc/api/config.md) system
* Simple [prefs storage](https://github.com/trbflxr/ksl/blob/master/doc/api/prefs.md) system
* Mods [synchronization](https://github.com/trbflxr/ksl/blob/master/doc/api/sync.md) for multiplayer games
* KSL manager auto updater
* Backward compatibility with BepInEx and legacy Kino mods
* Developer console
* Simple network debug tools for developers

## Developers guide

Download KSL SDK [here](https://github.com/trbflxr/ksl_sdk).

Mods and extensions creation [documentation](https://github.com/trbflxr/ksl/blob/master/doc/guide/dev/sdk.md).

## Questions, suggestions and games support

If you have any questions or suggestions or the loader doesn't work on your game, please contact **trbflxr** @Discord.

In case the game you're trying to mod uses the **Unity mono** runtime but KSL doesn't work with it, contact me on Discord and we'll work something out.

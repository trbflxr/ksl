# KSL SDK documentation

---

Using KSL you can make mods and extensions for Unity mono games.

[Mods](mods.md) are used to extend or modify the game itself.

[Extensions](extensions.md) are used to extend KSL functional. Mainly used as a "bridge" between game and the loader to make the loader more integrated in the game.

KSL featuring 2 types of mods / extensions:

* **Public** - Are available for all users
* **Private** - SteamID locked for whitelisted users only

> Before you start developing mods / extensions, you need to get **developer rights**. Read more about getting the rights [here](developer_rights.md).

> Also make sure you have KSL devtools and SDK downloaded. You can get it [here](https://github.com/trbflxr/ksl_sdk).

## Setup Project

Learn how to setup the project to start the mod / extension development for KSL [here](setup_project.md).

## Create mod / extension

When all is setup and configured you can start developing [mods](mods.md) and [extensions](extensions.md).

KSL also features [Harmony](https://github.com/pardeike/Harmony) patches to allow for a more extended game modification.
Learn more about Harmony [here](https://harmony.pardeike.net/).

## Setup KSL updater

To keep your mod / extension updated learn more about [KSL updater](updater.md).

## Build mod / extension

Mods and extensions for KSL have to be built using KSL maykr tool.

Learn more about build process [here](maykr.md).

> Make sure you have [developer rights](developer_rights.md) before building the mod / extension. Otherwise you will not be able to [generate a key](control_panel.md) for the mod / extension.

## Publish release

When your build is ready learn how to publish it [here](publish.md).

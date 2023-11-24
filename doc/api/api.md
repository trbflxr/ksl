# KSL documentation

KSL API also features an in-code documentation. Get the [SDK](https://github.com/trbflxr/ksl_sdk).

## Base classes and meta

Both mods and extensions must have a [KSLMeta](#kslmeta) attribute and have to be inherited from [BaseMod](#basemod) or [BaseExtension](#baseextension) classes. More about it bellow.

Also consider checking out an [example](#examples) project.

---

### [KSLMeta](https://github.com/trbflxr/ksl/blob/master/doc/api/ksl_meta.md)

Metadata required by KSL. Mods as well as extensions are required to have this attribute.

---

### [BaseMod](https://github.com/trbflxr/ksl/blob/master/doc/api/base_mod.md)

Base class for KSL mods.

---

### [BaseExtension](https://github.com/trbflxr/ksl/blob/master/doc/api/base_extension.md)

Base class for KSL extensions.

---

## Interfaces

### [ISyncProvider](https://github.com/trbflxr/ksl/blob/master/doc/api/isyncprovider.md)

Synchronization provider interface. You can only implement it for [extensions](https://github.com/trbflxr/ksl/blob/master/doc/guide/dev/extensions.md). Needed to provide synchronization for KSL mods in multiplayer games.

---

## API

All API entrypoints are located in the **KSL.API** namespace in the static class **Kino**.

KSL API project features an in-code documentation. Bellow you will find a more in-depth guide with additional information and examples.

---

### [Log](https://github.com/trbflxr/ksl/blob/master/doc/api/log.md)

The log API used to log messages in **KSL format**. Also default **Unity.Debug** can be used for logging however is not recommended.

---

### [Loader](https://github.com/trbflxr/ksl/blob/master/doc/api/loader.md)

The loader API used to get loaded mods / extensions lists and to unload current mod.

---

### [Prefs](https://github.com/trbflxr/ksl/blob/master/doc/api/prefs.md)

Simple prefs storage interface allowing you to save and load values. However it only supports the following list of [types](https://github.com/trbflxr/ksl/blob/master/doc/api/prefs.md#supported-types).

In case if you need a more advanced way to store the mod / extension config values, consider using the [Config](#config) interface.

---

### [Config](https://github.com/trbflxr/ksl/blob/master/doc/api/config.md)

The configuration API used to create the mod / extension configs and custom type parsers. This is an advanced way to store the mod / extension config values.

In case if you need a simple key-value storage, consider using [Prefs](#prefs) interface.

---

### [Input](https://github.com/trbflxr/ksl/blob/master/doc/api/input.md)

The input manager API can be used to bind hotkeys for mods and extensions (hotkeys are re-bindable).

---

### [UI](https://github.com/trbflxr/ksl/blob/master/doc/api/ui.md)

The UI API used to draw mods / extensions, push or pop contexts and more.

---

### [Paths](https://github.com/trbflxr/ksl/blob/master/doc/api/paths.md)

Nothing special, just a paths holder.

---

### [Utils](https://github.com/trbflxr/ksl/blob/master/doc/api/utils.md)

Utility methods.

---

### [Callbacks](https://github.com/trbflxr/ksl/blob/master/doc/api/callbacks.md)

Container for KSL callbacks.

---

### [Info](https://github.com/trbflxr/ksl/blob/master/doc/api/info.md)

Application and user info interface.

---

### [Sync](https://github.com/trbflxr/ksl/blob/master/doc/api/sync.md)

An interface that allows you to add synchronization for your mods and extensions.  
Provided that there are extensions for the game that provide a synchronization interface

---

# Examples

Download and explore KSL example project [here](https://github.com/trbflxr/ksl_sdk).

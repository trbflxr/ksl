﻿# KSL documentation

KSL API also features an in-code documentation. Get the [SDK](https://github.com/trbflxr/ksl_sdk).

## Base classes and meta

Both mods and extensions must have a [KSLMeta](api.md#kslmeta) attribute and have to be inherited from [BaseMod](api.md#basemod) or [BaseExtension](api.md#baseextension) classes. More about it bellow.

Also consider checking out an [example](api.md#examples) project.

---

### [KSLMeta](ksl_meta.md)

Metadata required by KSL. Mods as well as extensions are required to have this attribute.

---

### [BaseMod](base_mod.md)

Base class for KSL mods.

---

### [BaseExtension](base_extension.md)

Base class for KSL extensions.

---

## API

All API entrypoints are located in the **KSL.API** namespace in the static class **Kino**.

KSL API project features an in-code documentation. Bellow you will find a more in-depth guide with additional information and examples.

---

### [Log](log.md)

The log API used to log messages in **KSL format**. Also default **Unity.Debug** can be used for logging however is not recommended.

---

### [Loader](loader.md)

The loader API used to get loaded mods / extensions lists and to unload current mod.

---

### [Prefs](prefs.md)

Simple prefs storage interface allowing you to save and load values. However it only supports the following list of [types](prefs.md#supported-types).

In case if you need a more advanced way to store the mod / extension config values, consider using the [Config](#config) interface.

---

### [Config](config.md)

The configuration API used to create the mod / extension configs and custom type parsers. This is an advanced way to store the mod / extension config values.

In case if you need a simple key-value storage, consider using [Prefs](#prefs) interface.

---

### [Input](input.md)

The input manager API can be used to bind hotkeys for mods and extensions (hotkeys are re-bindable).

---

### [UI](ui.md)

The UI API used to draw mods / extensions, push or pop contexts and more.

---

### [Paths](paths.md)

Nothing special, just a paths holder.

---

### [Utils](utils.md)

Utility methods.

---

### [Callbacks](callbacks.md)

Container for KSL callbacks.

---

### [Info](info.md)

Application and user info interface.

---

# Examples

Download and explore KSL example project [here](https://github.com/trbflxr/ksl_sdk).
# KSLMeta

This is a metadata for KSL mod / extension. All mods and extensions have to have this attribute.

```c#
[KSLMeta("ModName", "1.0.0", "trbflxr")]
public class MyMod : BaseMod {
    ...
}
```

The attribute have 3 string parameters:

* **modName** - the name of the mod that will be displayed in the KSL mods menu
* **version** - version of the mod that is also used by [updater](../guide/dev/updater.md)
* **author** - an author or a team that created the mod

> [!IMPORTANT]  
> Version has to be in the following format: **major.minor.patch**

## Getters

### Name

```c#
public string Name { get; }
```

### Version

```c#
public System.Version Version { get; }
```

### Author

```c#
public string Author { get; }
```

### Guid

```c#
public string Guid { get; }
```

# KSL Loader

### Name

```c#
string Name { get; }
```

Getter for KSL loader name with version

### RequestUnloadSelf

```c#
void RequestUnloadSelf();
```

This method is used to unload the mod that called this function

Example usage:

```c#
private void UnloadTheMod() {
  Kino.Loader.RequestUnloadSelf();
}
```

### IsModLoadedWithName

```c#
bool IsModLoadedWithName(string modName);
```

This method is used to check if the mod or extension with name are loaded. See also [IsModLoadedWithGuid](loader.md#ismodloadedwithguid)

Example usage:

```c#
public override void OnStart() {
  if (Kino.Loader.IsModLoadedWithName("ExampleMod")) {
    Kino.Log.Info("ExampleMod found");
  }
}
```

### IsModLoadedWithGuid

```c#
bool IsModLoadedWithGuid(string modGuid);
```

This method is used to check if a mod or an extension with GUID are loaded. See also [IsModLoadedWithName](loader.md#ismodloadedwithname)

Example usage:

```c#
public override void OnStart() {		
  if (Kino.Loader.IsModLoadedWithGuid("Author.TestMod")) {
    Kino.Log.Info("TestMod found");
  }
}
```

### GetLoadedMods

```c#
List<KSLModMeta> GetLoadedMods();
```

Getter for loaded mods and extensions

Example usage:

```c#
public override void OnStart() {
  var mods = Kino.Loader.GetLoadedMods();
  foreach (var mod in mods) {
    Kino.Log.Info($"{mod.Name} v{mod.Version} by {mod.Author}");
  }
}
```

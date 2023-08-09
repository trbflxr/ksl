# BaseMod

This is a base class for KSL mods. All mods should be inherited from it.

> [!NOTE]  
> Keep in mind that this class inherits from MonoBehaviour so you can use Unity event methods in it.

## Getters

### Location

```c#
public string Location { get; internal set; }
```

Path to the mod file on disc

---

### Meta

```c#
public KSLMeta Meta { get; internal set; }
```

Metadata. Learn more about it [here](ksl_meta.md)

---

## Virtual methods

### OnUIDraw

```c#
public virtual void OnUIDraw() { }
```

Draw all mod UI in this method. It will be called if you select the mod in the main menu.
You can draw UI using [KSL UI](ui.md) or using default unity GUI or GUILayout.

---

### OnAdditionalAboutUIDraw

```c#
public virtual void OnAdditionalAboutUIDraw() { }
```

Additional UI for the "About" context. It will be called if you navigate to "About" context of the mod.
You can draw UI using [KSL UI](ui.md) or using the default unity GUI or GUILayout.

---

### GetIcon

```c#
public virtual Texture2D GetIcon() { return null; }
```

Override this method if you want to set a custom icon for the mod.

> [!NOTE]  
> See example of setting a custom icon below.

```c#
public override Texture2D GetIcon() {
  var assembly = Assembly.GetExecutingAssembly();
  return Kino.Utils.LoadEmbeddedTexture(assembly, "KSL.CarX.Resources.icon.png");
}
```

---

# BaseExtension

This is a base class for KSL extensions. All extensions should be inherited from it.

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

### Behaviour

```c#
public MonoBehaviour Behaviour { get; internal set; }
```

Getter for parent MonoBehaviour object

---

## Virtual methods

### OnStart

```c#
public virtual void OnStart() { }
```

This is an "initialization" method it will be called once on extension init

---

### OnDestroy

```c#
public virtual void OnDestroy() { }
```

This is an "deinitialization" method it will be called once on extension deinit

---

### OnUpdate

```c#
public virtual void OnUpdate() { }
```

This method will be called in every game frame, same as a Unity Update event. See more at [Unity execution order](https://docs.unity3d.com/Manual/ExecutionOrder.html).

---

### OnLateUpdate

```c#
public virtual void OnLateUpdate() { }
```

This method will be called at the end of every game frame, same as a Unity LateUpdate event. See more at [Unity execution order](https://docs.unity3d.com/Manual/ExecutionOrder.html).

---

### OnFixedUpdate

```c#
public virtual void OnFixedUpdate() { }
```

This method will be called in the Unity FixedUpdate. See more at [Unity execution order](https://docs.unity3d.com/Manual/ExecutionOrder.html).

---

### OnSceneLoaded

```c#
public virtual void OnSceneLoaded(Scene scene, LoadSceneMode mode) { }
```

This method will be called when Unity scene is loaded.

---

### OnSceneChanged

```c#
public virtual void OnSceneChanged(Scene current, Scene next) { }
```

This method will be called on Unity scene change.

---

### OnUIDraw

```c#
public virtual void OnUIDraw() { }
```

Draw all mod UI in this method. It will be called if you select the mod in the main menu.
You can draw UI using [KSL UI](ui.md) or using the default unity GUI or GUILayout.

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

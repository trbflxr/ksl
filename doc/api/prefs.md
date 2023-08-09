# KSL Prefs storage

This is a simple way to store the mod / extension config values.

Every mod / extension has its own prefs storage. You don't have to set anything up and can use it immediately. However prefs storage supports only following [types](#supported-types).

If you need more advanced and flexible way to store the mod / extension values, consider using the [Config](config.md) interface.

### Supported types

* bool
* float
* int
* uint
* ulong
* string
* Unity.Vector2
* Unity.Vector3
* Unity.Rect

### Get\<T>

```c#
T Get<T>(string key, T defaultValue = default);
```

This method is used to get the value from the prefs storage. Where is **T** is one of [supported types](#supported-types).

> [!NOTE]  
> **Note:** If there is no value with specified **key** presented in the storage, then default value for the type will be returned. However you can explicitly specify the default value.

Example:

```c#
public override void OnStart() {
  float value1 = Kino.Prefs.Get<float>("my_float1");
  float value2 = Kino.Prefs.Get("my_float2", 5.0f);
}

```

### TryGet\<T>

```c#
bool TryGet<T>(string key, out T value, T defaultValue = default);
```

This method is used to get the value from the prefs storage and return it as an **out** parameter. It also returns a **bool** flag that represents if the value is found in the prefs storage or not.

**T** has to be one of [supported types](#supported-types).

Also you can specify explicit **defaultValue** so that if the value with the **key** was not found it will be created with that specific value.

Example:

```c#
public override void OnStart() {
  bool found1 = Kino.Prefs.TryGet<int>("my_int32_1", out int intValue1);
  bool found2 = Kino.Prefs.TryGet("my_int32_2", out int intValue2);
  bool found3 = Kino.Prefs.TryGet("my_int32_3", out int intValue3, 100);
}

```

### Set\<T>

```c#
bool Set<T>(string key, T value);
```

This method is used to save values to prefs storage by a provided **key**. It returns **true** if the value was saved without any errors.

> **Important:** Keep in mind that if you saved for example an **int** with key **my_key** and then you saved **Vector2** with the same **my_key** key the first value of **int** will be overridden. Keep your keys unique.

Example:

```c#
public override void OnStart() {
  bool saved1 = Kino.Prefs.Set("my_key", 123);
  bool saved2 = Kino.Prefs.Set<float>("my_float", 15.0f);
  bool saved3 = Kino.Prefs.Set("my_string", "Hello world!");

  // Save was called with "my_key" again. It will override first saved value with "my_key" which is 123:int.
  // Don't worry you will have a warning message in the logs.
  bool overridden = Kino.Prefs.Set("my_key", Vector3.one);
}
```

---

# KSL Config

More info on [config creation](config.md#iconfig) and [custom type parsers](config.md#typeparsert) below.

> Also consider checking out an [example KSL mod](https://github.com/trbflxr/ksl_sdk) to get a more detailed example.

This is an advanced way to save the mod / extension config values. If you need a simple way to store mod / extension data, consider using [Prefs storage](prefs.md).

Config takes more time to setup and understand but it also give you a flexible way to store custom types.

## IConfig

Config interface used to register configs for mods and extensions.

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
* Support for [custom types](config.md#registerparser)

### RegisterParser

```c#
IConfig RegisterParser<T>() where T : IInternalTypeParser, new();
```

Use this method if config(s) you want to register contain(s) custom types that are not listed in [types list](config.md#supported-types).

More info and how-to-use examples [here](config.md#custom-parser-registration).

### RegisterConfig

```c#
T RegisterConfig<T>(string customName = null) where T : class;
```

Method for config registration.
Keep in mind that if a config contains custom types which are not listed in [types list](config.md#supported-types) you have to call [RegisterParser](config.md#registerparser) and register a parser for it.

More [info and examples](config.md#config-registration) further down.

### Save

```c#
void Save<T>() where T : class;
```

Use this method for marking config of type **T** for save. The config will be written on the disc with slight delay so it is preferred to use in something like [sliders](ui.md#slider). Mainly is to be used after changing custom type values: [example](config.md#config-auto-and-manual-save).

### ForceSave

```c#
void ForceSave<T>() where T : class;
```

Use this method to trigger force save for config of type **T** without any delays. Mainly is to be used after changing custom type values: [example](config.md#config-auto-and-manual-save).

## TypeParser\<T>

Base class for custom type parsers.

### ToRawString

```c#
protected abstract string ToRawString(T value);
```

Method for converting custom type to a string. See [example](config.md#custom-type-parser-example) below.

### Parse

```c#
protected abstract T Parse(string rawData);
```

Method for parsing custom type from string. See [example](config.md#custom-type-parser-example) below.

> **Note:** Parse will be called with **null** value at first config initialization and for every new type you add to the config.
>
> So make sure you have null check at the beginning of the method to properly initialize config values.

## Config example

Config has to be defined as a public **interface** and registered using [RegisterConfig](config.md#registerconfig) which will return an instance of a config that can be stored.

List of [supported types](config.md#supported-types). Also you can define [custom types](config.md#custom-type-parser-example) and register parsers using [RegisterParser](config.md#registerparser).

Registered configs have an auto-save functionality **only** for types from the [list](config.md#supported-types). [ForceSave](config.md#forcesave) custom types should be called after the value change. More about it [here](config.md#config-auto-and-manual-save).

Example config:

```c#
public interface ITestConfig {
  public CustomType CustomType { get; set; }
  public float Value { get; set; }
  public string Value2 { get; set; }
}
```

Example of a [CustomType](config.md#custom-type-parser-example) and a parser for it.

### Custom parser registration

If the config contains custom types which are not presented in the [supported types](config.md#supported-types) list parser registration should be done first.
Example of a custom type and a type parser can be found [here](config.md#custom-parser-registration).

To register a custom parser use the following example:

```c#
private void Start() {
  ...
  Kino.Config.RegisterParser<CustomTypeParser>();
  // register configs here
}
```

### Config registration

Keep in mind that if the config contains types that not presented in the [supported types](config.md#supported-types) list, [parser registration](config.md#custom-parser-registration) should be done first.

After registration config should be stored for future use.

Learn more about [config save system](config.md#config-auto-and-manual-save).

Example of a config registration:

```c#
public interface ITestConfig {
  public CustomType CustomType { get; set; }
  public float Value { get; set; }
  public string Value2 { get; set; }
}

public class ExampleMod : BaseMod {
  private ITestConfig config_;

  private void Start() {
    ...
    // because ITestConfig contains a custom type the parser for it should be registered first
    Kino.Config.RegisterParser<CustomTypeParser>();

    // config registration
    config_ = Kino.Config.RegisterConfig<ITestConfig>();
  }
}
```

A config can be registered without setting the name using [RegisterConfig](config.md#registerconfig), but you can only do it once. The config file will be named the same as the mod.
In a case that you need to create more then one config you have to explicitly specify names for them.

```c#
private void Start() {
  defaultConfig_ = Kino.Config.RegisterConfig<IDefaultConfig>();
  testConfig_ = Kino.Config.RegisterConfig<ITestConfig>("TestConfig");
}
```

### Config auto and manual save

For all config properties with a [supported type](config.md#supported-types) KSL will add a listener and on any property change the config will be marked for save.

If the config has [custom types](config.md#custom-type-parser-example) properties it will only be marked for save when setting a property value directly (example below). But in a case of setting a value to one of custom type's properties config will not be marked for save.

Auto-save example:

```c#
public interface ITestConfig {
  public CustomType CustomType { get; set; }
  public float Value { get; set; }
  public string Value2 { get; set; }
}

...

private void Start() {
  testConfig_ = Kino.Config.RegisterConfig<ITestConfig>();

  // ITestConfig will be marked to save
  // No need to call ForceSave
  testConfig_.Value = 1.0f;
}

```

Custom type value change:

```c#
public interface ITestConfig {
  public CustomType CustomType { get; set; }
  public float Value { get; set; }
  public string Value2 { get; set; }
}

...

private void Start() {
  testConfig_ = Kino.Config.RegisterConfig<ITestConfig>();

  // This action will trigger config auto-save because the value has been setted directly to the CustomType property
  testConfig_.CustomType = new CustomType();

  // Config will not be marked to save on changing CustomType's IntValue
  // In this case ForceSave should be called to mark the config to save
  testConfig_.CustomType.IntValue = 10;

  // Marking config to save
  Kino.Config.ForceSave<ITestConfig>();
}
```

## Custom type parser example

Keep in mind that this is an example using a custom type parser. You can define any logic you want, use this as an example.

```c#
// Custom type class. You can declare any types, but they need a custom parser, an example of which is below
public class CustomType {
  public float FloatValue;
  public int IntValue;
  public bool BoolValue;
}

// Custom type parser.
public class CustomTypeParser : TypeParser<CustomType> {
  // ToRawString used to define define how the type should be serialized as a string.
  // In this example I serialized 3 values with ' '(space) separator.
  protected override string ToRawString(CustomType value) {
    return $"{value.FloatValue:F3},{value.IntValue},{value.BoolValue}";
  }

  // Deserialization method.
  // In this example all 3 values are serialized in a string with ','(comma) separator.
  protected override CustomType Parse(string rawData) {
    // First create a result value
    var result = new CustomType();

    // If the string is null or empty returns the default value created before.
    // KSL will call Parse on first config initialization and for every new type in the config with null value
    if (string.IsNullOrWhiteSpace(rawData)) {
      return result;
    }

    // This example has 3 values in CustomType (float, int and bool),
    // Split the string into parts and if parts count does not equal 3, then return a default value.
    var parts = rawData.Split(',');
    if (parts.Length != 3) {
      return result;
    }

    // Parse values from a string.
    float.TryParse(parts[0], out result.FloatValue);
    int.TryParse(parts[1], out result.IntValue);
    bool.TryParse(parts[2], out result.BoolValue);

    // Return result value
    return result;
  }
}
```

# KSL Paths

The paths API is pretty self-explanatory

```c#
public string GameRoot { get; }

public string Mods { get; }
public string Extensions { get; }
public string Config { get; }
public string Cache { get; }
public string Dev { get; }

public string LoaderRoot { get; }

public string Managed { get; }

public string Executable { get; }
public string ProcessName { get; }

public string[] DllSearchPaths { get; }
```

> Keep in mind that **Dev** directory will only be created if you have enabled devtools in the KSL developer settings.

Example:

```c#
public override void OnStart() {
  Kino.Log.Info($"Game .exe location: {Kino.Paths.Executable}");
}
```

# Info interface

This interface can be used to get access to basic user and application info.

### SteamId

```c#
ulong SteamId { get; }
```

Getter for user's SteamID.

Example:

```c#
public override void OnStart() {
  Kino.Log.Info($"SteamID: {Kino.Info.SteamId}");
}

```

### AppId

```c#
uint AppId { get; }
```

Getter for current application ID. This id corresponds to steam application ID.

Example:

```c#
public override void OnStart() {
  Kino.Log.Info($"AppID: {Kino.Info.AppId}");
}

```

### AppName

```c#
string AppName { get; }
```

Getter for current application name.

Example:

```c#
public override void OnStart() {
  Kino.Log.Info($"AppName: {Kino.Info.AppName}");
}

```
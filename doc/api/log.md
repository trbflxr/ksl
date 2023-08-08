# KSL Log

The paths API is pretty self-explanatory. It works on same principals as Unity.Debug but is formatted for KSL.

Every mod and extension has its own dedicated logger.

```c#
void Fatal(object data);
void Error(object data);
void Warning(object data);
void Info(object data);
```

Example:

```c#
public override void OnStart() {
  Kino.Log.Info("Hello!");
  Kino.Log.Error("Oh no it's an error!");
}
```

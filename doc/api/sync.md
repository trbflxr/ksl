# Sync interface

An interface that allows you to add synchronization for your mods and extensions.  
Provided that there are extensions for the game that provide a synchronization interface

### IsAvailable

```c#
bool IsAvailable { get; }
```

Synchronization availability interface.

Example:

```c#
public override void OnStart() {
  Kino.Log.Info($"Sync available: {Kino.Sync.IsAvailable}");
}

```

### TryRegisterPacket

```c#
bool TryRegisterPacket(string packetName, out int packetId);
```

Try register new packet for current mod / extension

Example usage:

```c#
private void RegisterPacket() {
  bool result = Kino.Sync.TryRegisterPacket("test", out int packetId);
}
```

### SetCallback

```c#
bool SetCallback(int packetId, Action<IPacket> onPacketReceived);
```

Set callback for selected packet ID

Example usage:

```c#
private void RegisterCallback() {
  bool result = Kino.Sync.SetCallback(packetId, OnPacketReceived);
}

private void OnPacketReceived(IPacket packet) {
  Kino.Log.Info($"Received: {packet.Id}");
}
```

### CreatePacket

```c#
IPacket CreatePacket(int packetId);
```

Creates a IPacket instance with provided ID

Example usage:

```c#
private void CreatePacketExample() {
  var packet = Kino.Sync.CreatePacket(packetId);
  packet.WriteIn32(123);
}
```

### CreatePacket

```c#
IPacket CreatePacket(int packetId, byte[] data);
```

Creates a IPacket instance with provided ID and data buffer. Use it if you already have a byte array that you want to send.

Example usage:

```c#
private void CreatePacketExample() {
  byte[] data = GetPacketData();
  var packet = Kino.Sync.CreatePacket(packetId, data);
}
```

### SendToAll

```c#
bool SendToAll(IPacket packet);
```

Allows you to send a packet to all clients

Example usage:

```c#
private void SendToAllExample() {
  var packet = Kino.Sync.CreatePacket(packetId);
  packet.WriteIn32(123);

  bool result = Kino.Sync.SendToAll(packet);
}
```

### SendTo

```c#
bool SendTo(IPacket packet, ulong receiverId);
```

Allows you to send a packet to all clients

Example usage:

```c#
private void SendToExample() {
  var packet = Kino.Sync.CreatePacket(packetId);
  packet.WriteIn32(123);

  bool result = Kino.Sync.SendTo(packet, userId);
}
```

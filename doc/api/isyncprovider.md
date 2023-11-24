# ISyncProvider

Synchronization interface allows you to add a synchronization provider.  
Can only be implemented for [extensions](https://github.com/trbflxr/ksl/blob/master/doc/guide/dev/extensions.md). Extension have to be verified to work as sync provider.

## Methods

### TrySendToAll

```c#
bool TrySendToAll(IPacket packet)
```

Send a packet to all clients

---

### TrySendTo

```c#
bool TrySendTo(IPacket packet, ulong receiverId)
```

Send a packet to specified client ID

---

### SetPacketCallback

```c#
void SetPacketCallback(Action<int, byte[]> onPacketReceived)
```

This method will be called by KSL to set packet receive callback

---

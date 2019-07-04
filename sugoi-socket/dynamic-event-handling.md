---
description: Register and deregister events in run time.
---

# Dynamic event handling

As all of the Sugoi modules anything which can be achieve by decroators can also be achieved by simple methods.

The `SocketHandler` class provides us the right method for achieving this approach

## Register events

### registerSocketEvent method

This method allows us to register callback for an event - equivalent to `socket.on(event,callback)`

```typescript
registerSocketEvent<T=any>(event: string, 
                           callback: (socket: SocketIOStatic.Socket, data: T) => void, 
                           middlewares?: Array<ISocketMiddleware> | string, 
                           namespace: string = "/")
```

`event` - The event we want to bind the callback to.  
`callback` - The callback method  
`middlewares` - _0...n_ functions which should apply before the callback apply.  
`namespace` - The namespace the event is related to \(Default: "/"\)

### registerServerEvent method

Same as registerSocketEvent but related to server events - equivalent to `io.on(event,callback)`.

```typescript
registerServerEvent<T=any>(event: string, 
                           callback: (socket: SocketIOStatic.Socket, data: T) => void, 
                           middlewares?: Array<ISocketMiddleware> | string, 
                           namespace: string = "/")
```

`event` - The event we want to bind the callback to.  
`callback` - The callback method  
`middlewares` -  Array of _0...n_ functions which should apply before the callback apply.  
`namespace` - The namespace the event is related to \(Default: "/"\)

## Deregister events

### deregisterSocketEvent method

This method allows us to deregister callback for socket event - equivalent to `socket.removeListener(event,callbackToRemove)`

```typescript
deregisterSocketEvent(event: string);
```

`event` - The event name

### deregisterServerEvent method

This method allows us to deregister callback for server event - equivalent to `io.removeListener(event,callbackToRemove)`

```typescript
deregisterServerEvent(event: string);
```

`event` - The event name  



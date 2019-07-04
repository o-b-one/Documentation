---
description: Listening to events become simple with decorators
---

# Binding a function to event

## Overview

SugoiJS provide single line binding solution for binding a class method to socket event

## Bind socket events

Listening to socket events become simple with @SocketOn decorator

```typescript
@SocketOn(event: string, namespace: string = "/", ...middlewares:Array<ISocketMiddleware>)
```

`event` - The event name  
`namespace` - The related namespace which the socket should be related to.  
`middlewares` - _0...n_ arguments of middleware functions which should occur before the event callback function.

Another signature of this decorator is:

```typescript
@SocketOn(event: string, ...middlewares:Array<ISocketMiddleware>)
```

```typescript
type ISocketMiddleware = (socket:SocketIOStatic.Socket,data:any)=>Promise<any>|any
```

This decorator registers the function as a callback for an event.  
In case middlewares functions were passed, those methods will occur right before the callback  function.

### Example

```typescript
@SocketOn("message","/",(socket,data)=>{
    console.log("log message data: %s from socket id: %s",data,socket.id);
})
function messageHandler(socket,data){
    socket.to(data.room).emit('message',data.message)
}
```

You can bind one function to multiple events by use multiple `@SocketOn` decorators.

## Bind Server events

Listening to Socket events become simple with @SocketServerOn decorator

```typescript
@SocketServerOn(event: string, namespace: string = "/", ...middlewares:Array<ISocketMiddleware>)
```

`event` - The event name  
`namespace` - The related namespace which the socket should be related to.  
`middlewares` - _0...n_ arguments of middleware functions which should occur before the event callback function.

Another signature of this decorator is:

```typescript
@SocketServerOn(event: string, ...middlewares:Array<ISocketMiddleware>)
```

```typescript
type ISocketMiddleware = (socket:SocketIOStatic.Socket,data:any)=>Promise<any>|any
```



This decorator registers the function as a callback for an event.  
In case middlewares functions were passed, those methods will occur right before the callback  function.

### Example

```typescript
@SocketSererOn("connection","/",(socket,data)=>{
    console.log("log message data: %s from socket id: %s",data,socket.id);
})
function messageHandler(socket){
    socket.emit('connected',{msg:"welcome"})
}
```

You can bind one function to multiple events by use multiple `@SocketServerOn` decorators.


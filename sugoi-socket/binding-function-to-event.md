---
description: Listening to socket event become simple with @SocketOn method
---

# Binding function to event

SugoiJS socket module provides the `@SocketOn(event:string, namespace:string="/")` decorator.

This decorator registers the function as a callback for an event.

### Example

```typescript
@SocketOn('message')
function(data,socket){
    socket.to(data.room).emit('message',data.message)
}
```

You can bind one function to multiple events by use multiple `@SocketOn` decorators.


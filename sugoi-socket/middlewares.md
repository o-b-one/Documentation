---
description: Chain middlewares per socket event
---

# Middlewares

## Event level middleware

SugoiJS gives the ability to chain middlewares on event level by the `@SocketOn`  , `@SocketOnByHandler`, `@SocketServerOn` and `@SocketServerOnByHandler` decorators

### Setting a middleware

Each of the decorators get as many middlewares as you specify, those middlewares will apply in the same order you passed the.

#### Example

```typescript
@SocketOn("message","/",(socket,data)=>{
    console.log("log message data: %s from socket id: %s",data,socket.id);
})
function messageHandler(socket,data){
    socket.to(data.room).emit('message',data.message)
}
```

{% hint style="info" %}
In case value was returned \(!= undefined\) from the middleware method, this value will be be passed to next middleware and evently to the action method itself.
{% endhint %}



### Break the middlewares chain

Since middlewares are sequential, you can use them to verify the data and break the flow whenever is needed.  
By using the `BreakMiddleware` method

```typescript
export function BreakMiddleware(reason?:any);
```

`reason` - The data which should be added to the exception.

#### Example

```typescript
@SocketOn("message","/",
(socket,data)=>{
    console.log("log message data: %s from socket id: %s",data,socket.id);
},
(socket,data)=>{
    if(!data.message)
        BreakMiddleware("No message property");
})
function messageHandler(socket,data){
    socket.to(data.room).emit('message',data.message)
}
```


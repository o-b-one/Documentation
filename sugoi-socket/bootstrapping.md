---
description: Setting up a socket server
---

# Bootstrapping

## Initialize socket server 

Setting up the socket server done by the `socketService.init` method:

### By existing server

```typescript
  socketService.init(serverInstance:http.Server|express.Application,
                     namespace:string ="/",
                     socketConfig?:socketOptions,
                     connectionCallback?:(socket)=>void,
                     disconnectCallback?:(socket)=>void
):SocketIOStatic.Server;
```

### By port



```typescript
  socketService.init(portNumber:number,
                     namespace:string ="/",
                     socketConfig?:socketOptions,
                     connectionCallback?:(socket)=>void,
                     disconnectCallback?:(socket)=>void
):SocketIOStatic.Server;
```

### Example

```typescript
import {SocketHandler} from "@sugoi/socket";

// serverInstance is server instance (sugoijs, express, koa, nodejs http etc.)
// in case you are using @socket\server, the instance returns from the 'listen' method
// signature - init(HttpServer: any, socketConfig: SocketIOStatic.ServerOptions, namespace: string): SocketIOStatic.Server
const SocketHandler = socketService.init(serverInstance);
```

### For ServerModule

Server module provide the ability to initiate services on the module initialization. Since socketServer is depended on the initialized http server instance we can delay it creation by using factory, this will be done by intercept the init method with an arrow function.

#### Example

```typescript
import {SocketHandler} from "@sugoi/socket";
import {serverInstance} from "../app";

@ServerModule({
    services: [{
            provide: () => SocketHandler.init(serverInstance),
            useName: "SocketServer"
        }]
})
export class BoostrapModule{
    constructor(@Inject("SocketServer") private _socketServer){}
}
```

## Init parameters

`serverInstance` =  The server instance the socket server should be attached to.  
`socketConfig?:socketOptions` - The socket server configurations with the same interface as on [socket.io documentation](https://socket.io/docs/server-api/)

```typescript
 socketOptions:{
      path: string,
      serveClient: boolean,
      adapter:Adapter,
      origins:string,
      parser:Parser
 }
```

`namespace:string`- The socket server namespace to bind to, allow to assign different endpoint to the socket server, more info on [socket.io documentation](https://socket.io/docs/rooms-and-namespaces/).

## Returned value

The returned value of the `SocketHandler.init` method is the socket server instance \(`SocketIOStatic.Server`\).


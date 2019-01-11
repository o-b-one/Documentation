---
description: Setting up the socket server
---

# Bootstrapping

## Initialize socket server 

Setting up the socket server done by the `socketService.init` method:

```typescript
  socketService.init(serverInstance:express.Application,
                     namespace:string ="/",
                     socketConfig?:socketOptions,
                     connectionCallback?:(socket)=>void,
                     disconnectCallback?:(socket)=>void
):SocketIOStatic.Server;
```

### Example

```typescript
import {SocketHandler} from "@sugoi/socket";

// serverInstance is express\koa instance
// in case you are using @socket\server, the instance returns from the 'listen' method
// signature - init(HttpServer: any, socketConfig: SocketIOStatic.ServerOptions, namespace: string): SocketIOStatic.Server
const SocketHandler = socketService.init(serverInstance);
```

### Init parameters

`serverInstance` = Express\Koa server instance

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

### Returned value

The returned value of the `SocketHandler.init` method is the socket server instance \(`SocketIOStatic.Server`\).


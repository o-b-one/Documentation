---
description: Getting the socket server instance
---

# Socket server instance

As mentioned on the bootstrapping section, the returned value of the `init`  method is the socket server instance, although there is another way to get the instance of the server.

#### `socketService.getSocketServerByNamespace(namespace:string)`

The `getSocketServerByNamespace` method returns the socket server instance which fit the  given namespace\(should be similar to the one who pass on the `init` method\), in case no server instance found for the given namespace null will be returned.


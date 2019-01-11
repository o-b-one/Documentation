---
description: Getting the socket server instance
---

# Socket server instance

As mentioned on the bootstrapping section, the returned value of the `init`  method is the socket server instance.   
Although,  there is another way to get the instance of the server.

#### `SocketHandler.getHandler(id?:number).getServer()`

The `getHandler` method returns the socket server instance which fit the  given id, the id is stored under the returned server instance of the init process and can be retrieved by the `getInstanceId` method.   
In case no id passed, the first initialized socket server instance will be returned

In case no server instance found for the given id null will be returned.




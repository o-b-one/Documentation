---
description: Getting the socket server instance
---

# Handling server & namespace

## Get server instance

As mentioned on the bootstrapping section, the returned value of the `init`  method is socket server instance.   
Although,  there are few more way to get the instance of the server.

### GetHandler\(\) method

The `getHandler` method returns the socket handler object which fits the given id. The handler later can be use for retrieving the socket server instance.

The handler id is stored under the returned server instance of the init process and can be retrieved by the `getInstanceId()` method. 

In case no id passed, the first initialized socket server instance will be returned

In case no server instance found for the given id `null` will be returned.

#### Example

`SocketHandler.getHandler(id?:string).getServer()`

### socket.getSocketServer\(\) method

Each socket which pass to the callback, contains the `getSocketServer()` method. this method returns the socket server instance

## Get namespace instance

Another important object is the namespace instance, this object allows to communicate with sockets under the same namespace.

### GetHandler\(\) method

Similar to the way we retrieve the server instance, we can use the `getHandler` method for retrieve the SocketHandler object, afterwards we will apply the `getNamespace(namespace:string)` for getting socket.io namespace object.

#### Example

`SocketHandler.getHandler(id?:string).getNamespace("/")`

### socket.getSocketNamespace\(\) method

Each socket which pass to the callback, contains the `getSocketNamespace()` method. this method returns the socket server instance


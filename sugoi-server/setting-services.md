---
description: Singleton services for easy data manipulation
---

# Setting services

## Overview

Service is a singleton class instance which able to be used by any class using injection.

## Defining class as a service

For setting class as a service the class must be decorated with the `@Injectable()` decorator, this will set the class as singleton.

```typescript
@Injectable()
class MyService{
    public listeners:number = 0;

    public incListeners(){
        this.listeners++;
    }

    public decListeners(){
        this.listeners--;
    }
}
```

The service need to be set on the module services array:

```typescript
@ServerModule({
    services: [MyService]
})
export class MyModule{
    constructor(){}
}
```

later we will be able to inject the service instance.

{% hint style="warning" %}
Service constructor cannot be defined with any arguments that are not injectable.
{% endhint %}



## **Variable binding - Injection**

* `@Inject(MyService) private myService:MyService`
* `@Inject("MyService") private myService:MyService`
* `constructor(private myService:MyService)`

  \*\*\*\*

### **Retrieve value from the "container"**

The [InversifyJS container](https://github.com/inversify/InversifyJS/blob/master/wiki/container_api.md) is handling and storing singleton objects.  
The container is stored on the server instance, each request and the `ServerContainerService`

### Retrieve the container object

We are able to retrieve the singleton class instance using the following methods:

* `<HttpServer>server.container`
* `req.container`
* `ServerContainerService.getContainerById(serverInstanceId)` - Using the _HttpServer_ object instanceId.

### Retrieve service instance

After retrieving the container we able to get the service instance as following:

* `private myService:MyService = container.get(MyService)`

#### Or

* `private myService:MyService = container.get("MyService")`

### 

## Injection types and aliasing

### Overview

Using the module services we are able to define singleton services, constant values and factories for easy injection.

The module services support more informative data structure

```typescript
{
    provide: Class |Factory method| Value,
    useName: string,
    type?:"constant"|"singleton"|"factory" // usually resolved automatically
}
```

{% hint style="info" %}
**Injection remains the same for all types**
{% endhint %}

### Examples

#### Singleton

Useful for getting the same instance of a class

```typescript
@ServerModule({
    services: [
        MyService,
        {
            provide: MyNewService,
            useName: "MyServiceV2"
        }
    ]
})
export class MyModule{
    constructor(){}
}
```

#### Factory

Useful for getting different instances of the same class

```typescript
@ServerModule({
    services: [
        MyService,
        {
            provide: () => new MyService(),
            useName: "MyServiceFactory"
        }
    ]
})
export class MyModule{
    constructor(){}
}
```

#### Constant

Useful for services instances \(Redis, Socket e.g.\) and configuration values

```typescript
@ServerModule({
    services: [
        MyService,
        {
            provide: SocketService.init(server),
            useName: "SocketServer"
        }
    ]
})
export class MyModule{
    constructor(){}
}
```


---
description: Singleton services for easy data manipulation
---

# Setting services \(Injectables\)

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
            provide: socketServer,
            useName: "SocketServer"
        }
    ]
})
export class MyModule{
    constructor(){}
}
```

\*\*\*\*

## \*\*\*\*

### 




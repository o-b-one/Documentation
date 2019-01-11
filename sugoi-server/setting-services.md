---
description: Singleton services for easy data manipulation
---

# Setting services

### Define class as singleton

For setting class as service the class must be decorated with `@Injectable` decorator, this will set the class as singleton.

```text
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



```text
@ServerModule({
    services: [MyService]
})
export class MyModule{
    constructor(){}
}
```

later we will be able to inject the service instance.

### **Variable binding**

* `@Inject(MyService) private myService:MyService`
* `@Inject("MyService") private myService:MyService`
* `constructor(private myService:MyService)`

  \*\*\*\*

### **Returning the value from the "container"**

The [InversifyJS container](https://github.com/inversify/InversifyJS/blob/master/wiki/container_api.md) is handling the singleton objects.

The container is stored on the server instance, each request and the `ServerContainerService` by the instanceId, so it can be reached in the following ways:

* `server.container`
* `req.container`
* `ServerContainerService.getContainerById(serverInstanceId)`

After retrieving the container we will able to get the service instance as following:

* `private myService:MyService = container.get(MyService)`
* `private myService:MyService = container.get("MyService")`

### 

### 




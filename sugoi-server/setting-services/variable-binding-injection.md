# Variable binding \(Injection\)

* `@Inject(MyService) private myService:MyService`
* `@Inject("MyService") private myService:MyService`
* `constructor(private myService:MyService)`

  \*\*\*\*

### **Retrieve value from the "container"**

The [InversifyJS container](https://github.com/inversify/InversifyJS/blob/master/wiki/container_api.md) is handling and storing singleton objects.  
The container is stored on the server instance, each request and the `ServerContainerService`

### Retrieve the container object

{% hint style="info" %}
Check the previous section \(Dynamic injectables\)
{% endhint %}

### Retrieve service instance

After retrieving the container we able to get the service instance as following:

* `private myService:MyService = container.get(MyService)`

#### Or

* `private myService:MyService = container.get("MyService")`


---
description: >-
  Registration can be done in run time using the container 'bind' method.The
  bind method allows to bind a class\function\value to a property.
---

# Dynamic injectables

### Retrieve the container object

We are able to retrieve the singleton class instance using the following methods:

* `<HttpServer>server.container`
* `req.container`
* `ServerContainerService.getContainerById(serverInstanceId)` - Using the _HttpServer_ object instanceId.
* Retrieve container by `Injector` class \(an injectable Proxy for container\)
  * @Inject\('Injector'\) injector: Injector
  * constructor\(injector: Injector\) 

### Example

`server.container.bind('HttpHandler').to(Http);`

`server.container.bind('DBConfig').toConstant({ip: 10.10.10.10});`

`server.container.bind('Human').toFactory(()=>new Human());`

`const newHuman = injector.get<Human>('Human');`


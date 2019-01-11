---
description: Module is the key for microservices approach
---

# Setting a module

Creating a module requires you to use the `@ServerModule` decorator.

The `@ServerModule`, get an object of the following structure:

`{`

   `controllers?:Class[],`

   `services?:Class[],`

   `modules?: Class[]`

`}`



Example:

```text
import {ServerModule} from "@sugoi/server"

@ServerModule({
    controllers:[CoreController],
    services: [CoreService],
    modules:[LoginModule,DashboardModule]
})
export class BootstrapModule{
    constructor(){}
}
```


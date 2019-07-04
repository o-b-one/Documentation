---
description: >-
  Delay module initialization for resource establish, configuration fetching
  e.g.
---

# Delay module initialization

## Overview

Whenever a module initialized all of it services will automatically be initialized with all of their dependencies.  
This solution allow you to delay this initialization until the resource will be available.

## Set delay loading

For setting a delay loading all need to be done is implementing the `IServerModule` interface.

This interface expose the `onLoad` method which returns a promise. As soon the promise will be resolved the module initialization will continue.

### Example:

```typescript
import {IServerModule, ServerModule} from "@sugoi/server"
import {ConfigHandler} from "@app/configuration/handler";

@ServerModule({
    controllers:[CoreController],
    services: [CoreService],
    modules:[LoginModule,DashboardModule]
})
export class BootstrapModule imlements IServerModule{
        constructor(private injector: Injector){
        }
         
       public async onLoad(): any | Promise<any> {
            const configHandler = this.injector.get<ConfigHandler>(ConfigHandler);
            return await configHandler.populate();
        }
}
```


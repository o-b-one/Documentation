---
description: Module is the key for microservices approach
---

# Modules

## Overview

SugoiJS support modular approach for easy migration to micro-services architecture. Therefore, for using SugoiJS server you should define at least one module - the bootstrap module.

## Setting a Module

Creating a module requires you to create a class with `@ServerModule` decorator on it .

The `@ServerModule`, retrieve an object of the following structure:

`{  
   controllers?:Object[],  
   services?:Object[],  
   modules?: Object[]  
}`

Those property will later be use for declaring the module controllers,services and sub-modules.

### Example:

```typescript
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


---
description: REST based models
---

# RESTFUL model

## Overview

Models of this type don't have direct connection to the storage unit. Therefore, the communication is done by a single request each time and the connection is closed as soon as the request is completed.

Common usage is RESTful requests.

## Initialize

For setting model of this type all you need to do is:

1.  Extend the `ModelAbstract` class
2. Define the [CRUD Logic](setting-crud-logic.md)

### Example

```typescript
export class MicroServiceModel extends ModelAbstract{
    public name:string;
   
    @Primary()
    public id: string;
  
    constructor(name:string){
        super();
        this.name = name;
    }
    
    protected saveEmitter(options?: any): Promise<any> {
        return rp({
            method:"POST",
            body:this
        });
    }
     // other CRUD actions implementation 

}
```




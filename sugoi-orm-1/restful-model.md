---
description: REST based models
---

# RESTFUL model

Models of this type don't have direct connection to the storage unit.

The communication is done by a single request. The connection is closed as soon as the request is completed.

Common usage is restful requests.

For setting model of this type all you need to do is extend the `ModelAbstract` class

Example:

```typescript
export class MicroServiceModel extends ModelAbstract{
    public name:string;
    
    constructor(name:string){
        super();
        this.name = name;
    }

}
```


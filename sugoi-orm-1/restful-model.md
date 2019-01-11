---
description: REST based models
---

# RESTFUL model

Models of this type don't have direct connection to the storage unit.

The communication is done by a single request. The connection closes as soon as the request is completed.

Common usage is restful requests.

For setting model of those type all you need to do is extend the `ModelAbstract` class

Example:

```text
export class MicroServiceModel extends ModelAbstract{
    public name:string;
    
    constructor(name:string){
        super();
        this.name = name;
    }

}
```


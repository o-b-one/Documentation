---
description: Run methods after instance construct
---

# @PostConstruct\(\)

## Overview

The `PostConstruct` decorator set the method to be called on moment after instance construct

## Example



```typescript
export class AdminController {
    public firstName:string;
    public lastName:string;
    public fullName:string;
    
    constructor(firstName:string, lastName:string){
        this.firstName = firstName;
        this.lastName = lastName;
    }
    @PostConstruct()
    generaterFullName(){
        this.fullName = `${this.firstName} ${this.lastName}`;
    
    }
}
```


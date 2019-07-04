---
description: SugoiJS provides extendable exception (error) class for better error handling.
---

# Exception

SugoiJS provides base abstract exception \(error\) class which can be extended and used for exceptions handling

```typescript
SugoiError:{
    code:number;
    message:string;
    data:Array<any>;
}
```

Feel free to extend this class to identify your own errors by:

```typescript
switch(err.constructor.name){
    case "MySugoiError":
        //handled error
        break;
    default:
        throw err;
}
```

Or by:

```typescript
if( err instanceof MySugoiError){
    //handled error
}else{
    throw err;
}
```


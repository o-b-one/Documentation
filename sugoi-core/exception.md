---
description: SugoiJS provides extendable exception(error) class for better error handling.
---

# Exception

SugoiJS provides base abstract exception\(error\) class which can be extended and used for exceptions handling

```text
SugoiError:{
    code:number;
    message:string;
    data:Array<any>;
}
```

Feel free to extend this class to identify your own error by:

```text
switch(err.constructor.name){
    case "MySugoiError":
        //handled error
        break;
    default:
        throw err;
}
```

Or by:

```text
if( err instanceof MySugoiError){
    //handled error
}else{
    throw err;
}
```


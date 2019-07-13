---
description: Easy way to handle errors thrown from a metho
---

# @Catch - error handling

## Overview

The `@Catch()` decorator provides an easy way to handle errors thrown from any method.  
Also, it's provide a way to handle errors based on type

{% hint style="info" %}
`The @Catch decorator can be applied on class level or method level`
{% endhint %}

## Usage

The Catch decorator can be use with error types or without declaring on error types

`Catch(handler: (err: Error | SugoiError) => any)`

`Catch(handler: (err: Error | SugoiError) => any, ...errors: Array<string |Error | SugoiError>)`

### Catch all errors

```typescript
@Catch(() => null)// will handle all the Errors and return null in case of an error
export class DecoratorCatch{
    private static number: number = 1;
    private instanceNumber: number = 0;

    catchCheck(numberToCheck: number){
        if(numberToCheck === 0){
            throw new MyError('testing1',321);
        }
        else if(numberToCheck === 1){
            throw new MyError2('testing2',321);
        }
        else if(numberToCheck === 2){
            throw new Error('test generic error');
        }
        return this.instanceNumber;
    }
}
```

### Declaring error type

While declaring an error type only error types of those type will be handled by the handler method

#### Example

```typescript
@Catch(() => null,
 'MyError', MyError2)// will handle Errors of class 'MyError' only 
                     // or instance of MyError2
                     // Returns null in case of an error
export class DecoratorCatch{
    private static number: number = 1;
    private instanceNumber: number = 0;

    @Catch(function(err){
        console.log('catcher got an error', err);
        return this.instanceNumber - 1
    }, 'Error') // will handle Errors of class 'Error' only
    catchCheck(numberToCheck: number){
        if(numberToCheck === 0){
            throw new MyError('testing1',321);
        }
        else if(numberToCheck === 1){
            throw new MyError2('testing2',321);
        }
        else if(numberToCheck === 2){
            throw new Error('test generic error');
        }
        return this.instanceNumber;
    }
}
```


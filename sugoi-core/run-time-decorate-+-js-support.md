---
description: Apply decoration in run time
---

# Run time decorate \( + JS support\)

## Overview

Apply run time decoration is strong advantage of SugoiJS which gives us the flexibility to apply decorators in run-time, either if it because of conditions or lazy-loading.

Applying decorators in run-time provides us the ability to use decorators by pure JS files as well.

## Usage

### Decorate - Class decorator

For applying decorator method on a call we are able to call the sugoiJS `decorate` method

`decorateProperty(methodToApply, target)`

#### Example

```javascript
// Using ES6
import {Catch, decorate} from '@sugoi/core';
// Using nodeJS
const {Catch, decorate} = require('@sugoi/core');

class Validator(){
    static validate(item){
        if(!item.valid){
            throw new Error('Invalid')
        }
    }
}
decorate(Catch(()=>false),Validator);
```



### Decorate - Property decorator

For applying decorator method on class property we are able to call the sugoiJS `decorateProperty` method

`decorateProperty(methodToApply, target, property)`

#### Example

```javascript
// Using ES6
import {Catch, decorateProperty} from '@sugoi/core';
// Using nodeJS
const {Catch, decorateProperty} = require('@sugoi/core');

class Validator(){
    static validate(item){
        if(!item.valid){
            throw new Error('Invalid')
        }
    }
}
decorateProperty(Catch(()=>false), Validator, 'validate');
```


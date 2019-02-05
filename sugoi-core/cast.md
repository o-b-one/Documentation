---
description: Cast (Aka. clone) allow to cast any object to class instance
---

# Casting

Cast  allows to transform any object to class instance with all of the class functionalities including static methods and properties.

## Usage

### Interface

`cast(classType, data, applyConstructor:boolean = false)`

* `classInstance` - The typeof class we want to cast to.
* `data` -  The data should be cast.
* `applyConstructor` - identify if constructor method should apply \(default is `false`\)



Using cast can be done in two ways:

### Without applying the class constructor

In that case the data will cast into class instance but constructor method will not apply, which means auto populated properties won't initialize.

#### Example

{% code-tabs %}
{% code-tabs-item title="post.class.ts" %}
```typescript
export class Post{
    title: string;
    body: string;
    creation: string = "11/11";
    owner: string;

    constructor(owner:string){
        this.owner = owner;
    }
    print(){
        console.log(`${this.title} - ${this.body} - ${creation}`);
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="main.ts" %}
```typescript
import { cast } from "@sugoi/core";

const casted = cast(Post,{title:"wow",body:"Much body"});
// in that case creation and owner won't initialize
casted.print(); => "wow - Much body - undefined"
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### With applying the class constructor

In that case the data will cast into class instance and constructor method will apply, which means auto populated properties will initialize.

#### Example

{% code-tabs %}
{% code-tabs-item title="post.class.ts" %}
```typescript
export class Post{
    title: string;
    body: string;
    creation: string = "11/11";
    owner: string;

    constructor(owner:string){
        this.owner = owner;
    }
    print(){
        console.log(`${this.title} - ${this.body} - ${creation}`);
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="main.ts" %}
```typescript
import { cast } from "@sugoi/core";

const casted = cast(Post,{title:"wow",body:"Much body"});
// in that case creation and owner won't initialize
casted.print(); => "wow - Much body - 11/11"
```
{% endcode-tabs-item %}
{% endcode-tabs %}




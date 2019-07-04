---
description: Allow object to be treated as iterables
---

# @Iterable\(\)

With `iterable()` decorator objects can be treated as iterables,  which mean spread operations, find, filter and all others array methods are availble.

### Example

{% code-tabs %}
{% code-tabs-item title="some.class.ts" %}
```typescript
@Iterable()
export class someClass{
    value1: string = "test";
    value2: number = 42;
    objectValue: any = {name:"Me",role:"Programmer"}
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="main.ts" %}
```typescript
const sc = new someClass()
console.log(JSON.stringify([...sc]))
//["test",42,{"name":"Me","role":"Programmer"}] <- order is not mandatory
```
{% endcode-tabs-item %}
{% endcode-tabs %}


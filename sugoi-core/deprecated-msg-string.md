---
description: >-
  Deprecated decorator allows to identify method as deprecated by printing
  deprecation message to the console or throwing an exception
---

# @Deprecated



The deprecated decorator prints deprecation message for each usage of the the annotated method. Also, the deprecation decorator allows to throw an exception whenever the method use.



{% code-tabs %}
{% code-tabs-item title="@Derprecated interface" %}
```typescript
export function Deprecated();
export function Deprecated(msg: string);
export function Deprecated(throwException: boolean);
export function Deprecated(msg: string, throwException: boolean);
```
{% endcode-tabs-item %}
{% endcode-tabs %}



### Message pattern

The default message is of the pattern:

`%s.%s is deprecated` while first string is the class name and the second string is the method name, for example `Utils.guid` will identify the method `guid` under `Utils` class is deprecated.

{% code-tabs %}
{% code-tabs-item title="utils.class.ts" %}
```typescript

export class Utils{
    @Deprecated()
    public static guid(){
        //some old code
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### Modify message

The message pattern can be change by passing the wanted pattern to the decorator:

{% code-tabs %}
{% code-tabs-item title="utils.class.ts" %}
```typescript

export class Utils{
    @Deprecated("Method %s.%s is deprecated please use NewUtils.guid instead")
    public static guid(){
        //some old code
    }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}


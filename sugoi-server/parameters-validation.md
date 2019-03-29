---
description: With SugoiJS request parameters validation become easier
---

# Parameters validation

## Overview

SugoiJS provides easy, one line solution for validating the request, this by using the `@RequestSchemaPolicy` decorator.

The `RequestSchemaPolicy` is similar to server module socket`SocketSchemaPolicy` method.

SugoiJS server module uses @sugoi/core policies ability for supplying pre-defined policies

{% hint style="info" %}
SugoiJS re-export SchemaTypes, TPolicy, TComparableSchema, Policy, UsePolicy, ComparableSchema from "@sugoi/core";
{% endhint %}

{% hint style="info" %}
Further information can be found on the [@sugoi/core package documentation](https://sugoijs.com/#/documentation/core/index)
{% endhint %}

## RequestSchemaPolicy

{% code-tabs %}
{% code-tabs-item title="RequestSchemaPolicy - decleration" %}
```typescript
/**
 *  paramSchema         - req.params
 *  queryParamSchema    - req.query
 *  bodySchema          - req.body
 *  headersSchema       - req.headers
 **/
export function RequestSchemaPolicy(paramSchema: TComparableSchema);
export function RequestSchemaPolicy(paramSchema: TComparableSchema, queryParamSchema: TComparableSchema);
export function RequestSchemaPolicy(paramSchema: TComparableSchema, queryParamSchema: TComparableSchema, bodySchema: TComparableSchema);
export function RequestSchemaPolicy(paramSchema: TComparableSchema, queryParamSchema: TComparableSchema, bodySchema: TComparableSchema, headersSchema: TComparableSchema);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The `RequestSchemaPolicy` decorator use for validating the request, this whild using a valid schema for Request params, Query params, body, headers.

In case null will pass the value won't be check.

### Example:

```typescript
@Controller('/dashboard')
export class DashboardController {
    constructor() {
    }

    @HttpPost("/:id")
    @RequestSchemaPolicy(
    {"id": ComparableSchema.ofType(SchemaTypes.NUMBER)},
     null,
     {
     "role": ComparableSchema.ofType(
                                     {
                                         text: ComparableSchema
                                                 .ofType(SchemaTypes.STRING)
                                                 .setRegex("([A-Z])+","i")
                                     }
                                     )
     }
     )//body schema is {role:{text:string//with regex - /([A-Z])+/i}}
    getUser(@RequestParam("id") id:number, @RequestBody() body:{role:{text:string}}) {
        return User.findOne({id,role:body.role.text})
    }

}
```

## Validation per parameter type

### RequestParamsSchemaPolicy

For validating only the request parameters you can use `RequestParamsSchemaPolicy` 

```typescript
function RequestParamsSchemaPolicy(schema: TComparableSchema)
```

### RequestQueryParamsSchemaPolicy

For validating only the request query parameters you can use`RequestQueryParamsSchemaPolicy` 

```typescript
function RequestQueryParamsSchemaPolicy(schema: TComparableSchema)
```

### RequestBodySchemaPolicy

For validating only the request body you can use`RequestBodySchemaPolicy`

```typescript
function RequestBodySchemaPolicy(schema: TComparableSchema)
```

### RequestHeadersSchemaPolicy

For validating only the request headers you can use `RequestHeadersSchemaPolicy`

```typescript
function RequestHeadersSchemaPolicy(schema: TComparableSchema)
```

### Full example

```typescript
    @HttpPost("/:id")
    @RequestParamsSchemaPolicy(RequestWithIDSchema)
    @RequestQueryParamsSchemaPolicy({
       check: ComparableSchema.ofType(SchemaTypes.STRING).setMandatory(false)
    })
    @RequestBodySchemaPolicy({
       data: ComparableSchema.ofType(SchemaTypes.STRING).setMandatory(true)
    })
    @RequestHeadersSchemaPolicy({
       "x-user-language":ComparableSchema.ofType(SchemaTypes.STRING).setMandatory(true)
    })
    public setData(@RequestParam("id") id: string) {
       // finally the logic
    }
```


---
description: With SugoiJS request parameters validation become easier
---

# Parameters validation

SugoiJS server module uses @sugoi/core policies and supply predefined policies, and re-export SchemaTypes, TPolicy, TComparableSchema, Policy, UsePolicy, ComparableSchema from "@sugoi/core";

Further information on the [@sugoi/core package documentation](https://sugoijs.com/#/documentation/core/index)

## RequestSchemaPolicy

```text
/**
 *  paramSchema         - req.params
 *  queryParamSchema    - req.query
 *  bodySchema          - req.body
 *  headersSchema       - req.headers
 **/
RequestSchemaPolicy(paramSchema?: TComparableSchema,queryParamSchema?: TComparableSchema,bodySchema?: TComparableSchema,headersSchema?: TComparableSchema)
```

The `RequestSchemaPolicy` decorator use for validate the request is using a valid schema for params\queryParams\body\headers.

In case null will pass the value won't check.

### Example:

```text
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


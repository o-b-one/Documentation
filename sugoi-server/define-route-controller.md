---
description: Setting up a route for your application
---

# Define a route \(Controller\)

## Define a route

To define a the root of your route use the `@Controller("/rootPath")` decorator.

For example for `"/dashboard/find"` and `"/dashboard/update"`,  the root of the route is dashboard.

To define sub path \(`"/find"` or `"/update"`\), use `@HttpGet`, `@HttpPut`, `@HttpDelete`, `@HttpPost` and the route as parameter.

## Handling the request

{% hint style="info" %}
SugoiJS uses inversify-express-utils decorators and re-export them.
{% endhint %}

For handling the request there are some decorator which can be us as the functions' arguments:

1. `@RequestParam(paramName?:string) param` - will return the parameters\ parameter under this property, if none found, null will be returned.
2. `@QueryParam(paramName?:string) qParam` - will return the query parameters\ parameter under this property, if none found, null will be returned.
3. `@RequestBody() body` - The body of the request
4. `@Cookies(cookieName:string) cookie` - The cookie which fits to the name, if none found, null will be returned.
5. `@RequestHeaders(headerName:string)` - The header which fits to the name, if none found, null will be returned.
6. `@Response()` - The response object.
7. `@Request()` - The request object.

## Handling the response

The response of the request will be whatever returned from the function, in case of thrown exception, the exception will get into the error handler who set on the bootstrapping level.

Further information can be found under [_`Response handling`_](response-handling.md#response-handling) __section

## Example

```typescript
import {Controller,Response,HttpGet,RequestParam} from "@sugoi/server";

@Controller('/dashboard')
export class CoreController{
    constructor(){}

    @HttpGet("/:role")
    test(@RequestParam('role') role:string,
         @RequestHeader("role") headerRole:string){
        if(role === headerRole )
            return "authorized";
        else{
            throw new Error("unauthorized")
        }
    }
}
```

Further information can be found on [Inversify-express-utils documentation](https://github.com/inversify/inversify-express-utils)


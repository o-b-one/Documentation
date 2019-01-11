---
description: With SugoiJS Authorization check is that simple.
---

# Authorization

## Overview

```typescript
/**
 *  requiredRole: TStringOrNumber|TStringOrNumber[] - The required role(s)
 *  permissions: TStringOrNumber|TStringOrNumber[]  - The required premission(s)
 *  failedCode: number                              - The response code in case the policy will fail
 **/
Authorized(requiredRole: TStringOrNumber|TStringOrNumber[] = null, permissions: TStringOrNumber|TStringOrNumber[] = null, failedCode: number = 401)
```

The `Authorized` decorator use for validate if the user is authorized and in the right role & have the right permissions\(optional\).

In case null will pass the value won't be checked.

## Initialize

The Authorized policy will use the `AuthProvider` which pass while the server init: `init(boostrapModule: any, rootPath?: string, moduleMetaKey?: string, authProvider?: AuthProvider)`

The `AuthProvider` will init for each request, the `AuthProvider` holding the request headers & cookies.

## Example

{% code-tabs %}
{% code-tabs-item title="authorization.class.ts" %}
```typescript
export class Authorization extends AuthProvider<User> {


    /**
     * Verify if user is authorized
     *
     * Implemented dummy check for x-sug-demo header to be equal to "Wyn1RRR9PQJPaqYM"
     *
     * @returns {Promise<boolean>}
     */
    isAuthenticated(): Promise<boolean> {
        return Promise.resolve(this.headers["x-sug-demo"] === "Wyn1RRR9PQJPaqYM");
    }

    getUser(req?: e.Request, res?: e.Response, next?: e.NextFunction): Promise<any> {
        return this.details 
            ?   Promise.resolve(this.details)
            : UserService.getUser(UserService.getIdFromCookie(this.cookie))
                          .then((user:User)=>{
                            this.details = user;
                            return user;
                          })
    }

    isInRole(...roles: Array<string | number>): Promise<boolean> {
        return this.getUser().then(user=>roles.includes(user.role));

    }

    /**
    * Check if on of user has some of the permissions.
    **/
    isAllowedTo(...permissions: Array<string | number>): Promise<boolean> {
        return this.getUser().then(user=>permissions.some(permission=>user.permissions.includes(permission)));
    }

    isResourceOwner(resourceId: any): Promise<boolean> {
        return this.getUser().then(user=>Resources.checkIfOwner(resourceId,user.id));
    }

}
```
{% endcode-tabs-item %}

{% code-tabs-item title="app.ts" %}
```typescript
init(boostrapModule,"/",null, Authorization).build().listen(3000)
```
{% endcode-tabs-item %}

{% code-tabs-item title="dashboard.controller.ts" %}
```typescript
@Controller('/dashboard')
export class DashboardController {
    constructor() {
    }

    @HttpPost("/:id")
    @Authorized(["User","Admin"],"User.READ")
    @Authorized(null,"User.READ_BY_ID") // This case promise the user have both "User.READ" AND "User.READ_BY_ID" permissions
    getUser(@RequestParam("id") id:number, @RequestBody() body:{role:{text:string}}) {
        return User.findOne({id,role:body.role.text})
    }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

### \*\*\*\*

```typescript

```


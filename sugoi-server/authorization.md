---
description: With SugoiJS Authorization check is that simple.
---

# Authorization

## The @Authorized decorator

```typescript
/**
 *  requiredRole: TStringOrNumber|TStringOrNumber[] - The required role(s)
 *  permissions: TStringOrNumber|TStringOrNumber[]  - The required premission(s)
 *  failedCode: number                              - The response code in case the policy will fail
 **/
Authorized(requiredRole: TStringOrNumber|TStringOrNumber[] = null, permissions: TStringOrNumber|TStringOrNumber[] = null, failedCode: number = 401)
```

The `Authorized` decorator use for validate the user is Authorized and in the right role and permissions\(optional\).

In case null will pass the value won't check.

The Authorized policy will use the `AuthProvider` which pass while the server init: `init(boostrapModule: any, rootPath?: string, moduleMetaKey?: string, authProvider?: AuthProvider)`

The `AuthProvider` will init for each request, the `AuthProvider` holding the request headers & cookies.

## Example:

### **authorization.class.ts:**

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

### **app.ts:**

```typescript
init(boostrapModule,"/",null, Authorization)
```

```typescript
init(boostrapModule,"/",null, Authorization)
```

### **dashboard.controller.ts:**

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


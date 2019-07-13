---
description: >-
  CRUD (Create, Read, Update, Delete) controller gives you an easy way to
  implement CRUD endpoints based on an ORM model.
---

# CRUD Controller

## Overview

CRUD Controller provide a factory for creating CRUD endpoints based on ORM Module without coding.  
The CRUD Controller was created for reduce boilerplate implementation of CRUD endpoints



## CRUDControllerFactory

Using the `CRUDControllerFactory` we can create enpoints using an ORM Model, the ORM model should extend the @sugoi/ORM `ModelAbstract`

The `CRUDControllerFactory`  expose the `of(model: ModelAbstract, options?: ICRUDOptions)` method

#### Example

```typescript

@ServerModule({
    controllers: [
        CRUDControllerFactory.of(MyModel) // Will create '/MyModel' uri based endpoints
    ],
    services: [],
    modules: []
})
export class Bootstrap {
}
```

### Endpoints

#### GET '/'

The GET endpoint without any parameter used for searching based on query parameters.

#### GET '/:id'

The GET endpoint with an id parameter used for query based on id.

#### POST '/'

The POST endpoint will create a new record in DB based on the request body.

#### PUT '/:id'

The PUT endpoint will update the record in DB based on the id with the request body.

#### DELETE '/:id'

The DELETE endpoint will delete the record from DB based on the id.

### CRUDController Options

While creating a CRUD Controller we are able to pass some options to the factory for defining the endpoint, authorization, permissions and roles.

```typescript
{
    endpoint?: string;
    authorized?: boolean;
    permissions?: Array<string | number>; 
    roles?: Array<string | number>;
}
```

#### Example

```typescript
@ServerModule({
    controllers: [
        CRUDControllerFactory.of(MyModel,{
            endpoint: '/MyModelCrud', 
            authorized: true, 
            roles: [ROLES.ADMIN, ROLES.AUTHOR],
        }) // Will create '/MyModelCrud' uri based endpoints
    ],
    services: [],
    modules: []
})
export class Bootstrap {
}
```

### Set allowed methods

By default all of the CRUD endpoints are toggled on, we can change it by using the`setAllowedMethods(...methods: Array<HTTP_METHOD>` static method

#### Example

```typescript
@ServerModule({
    controllers: [
        CRUDControllerFactory.of(MyModel).setAllowedMethods(
                                HTTP_METHOD.GET,
                                HTTP_METHOD.POST,
                                HTTP_METHOD.PUT
                            )
    ],
    services: [],
    modules: []
})
export class Bootstrap {
}
```


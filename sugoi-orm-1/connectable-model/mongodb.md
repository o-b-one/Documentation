---
description: SugoiJS predefined module for mongoDB client
---

# MongoDB

[![npm version](https://badge.fury.io/js/%40sugoi%2Fmongodb.svg)](https://badge.fury.io/js/%40sugoi%2Fmongodb) [![Build Status](https://travis-ci.org/sugoiJS/mongoDB.svg?branch=master)](https://travis-ci.org/sugoiJS/mongoDB) [![codecov](https://codecov.io/gh/sugoiJS/mongoDB/branch/master/graph/badge.svg)](https://codecov.io/gh/sugoiJS/mongoDB)

## Overview

SugoiJS provides mongoDB client that is based on the ORM module with all of its' abilities.

## Bootstrapping

Bootstrapping is done by one line:

```typescript
MongoModel.setConnection(configuration:IConnectionConfig,connectionName:string = "default")
```

The `connectionName` parameter is used for multiple connection.

### Example

```typescript
import {MongoModel} from "@sugoi/mongodb";

MongoModel.setConnection({
                        port: 27017,
                        protocol: "mongodb://",
                        hostName: "my-mongo.services.com",
                        db: "myAuthDB", //authorization DB
                        user: "dbUser",
                        password: "dbPassword"
}, "adminDB");
```

## Creating a model

For creating a model, all you need to do is to extend the `MongoModel` class and define your properties.

### Example

```typescript
export class Message extends MongoModel {
    public userId:string;
    public body:string;

    constructor(userId:string,body:string){
        super();
        this.userId = userId;
        this.body = body;
    }
}
```

## Model naming

By default the model name is the class name \(case sensitive\).

For override the collection name, use the `@ModelName` decorator

### Example

```typescript
@ModelName("AppMessage")
export class Message extends MongoModel {
        public userId:string;
        public body:string;

    constructor(userId:string,body:string){
        super();
        this.userId = userId;
        this.body = body;
    }
}
```

## **Using connections**

For using different connection for a model you can use `setConnectionName` static method or `ConnectionName` decorator.

### Example

```typescript
@ModelName("AppMessage")
@ConnectionName("appDB")
export class Message extends MongoModel {
            public userId:string;
            public body:string;

    constructor(userId:string,body:string){
        super();
        this.userId = userId;
        this.body = body;
        this.constructor.setConnectionName("adminDB");
    }
}
```



For more information enter the @sugoi/orm page




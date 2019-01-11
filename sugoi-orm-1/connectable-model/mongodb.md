---
description: SugoiJS pre-defined module for mongoDB client
---

# MongoDB

SugoiJS provides mongoDB client which based on the ORM module with all of it's abilities.

## Bootstrapping

Bootstrapping done by only one line:

```text
MongoModel.setConnection(configuration:IConnectionConfig,connectionName:string = "default")
```

The `connectionName` parameter is used for multiple connection

### Example:

```text
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

to create a model, all you need is to extend the MongoModel class and set your properties.

Just like that:

```text
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

By default the collection name is the class name \(case sensitive\).

For override the collection name, use the @ModelName decorator:

```text
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

For using different connection for model you able to either use all you need to use `setConnectionName` static method or `ConnectionName` decorator.

```text
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



More information on the [@sugoi/mongoDB page](https://www.npmjs.com/package/@sugoi/mongodb)




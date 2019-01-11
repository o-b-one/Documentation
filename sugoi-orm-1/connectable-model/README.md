---
description: Models which are based on direct connection to DB
---

# Connectable model

Example \(by the [@sugoi/mongodb](https://www.npmjs.com/package/@sugoi/mongodb) package implementation\):

```text
import {Connection,ConnectableModel} from "@sugoi/orm";

export class MongoModel extends ConnectableModel{
    protected static ConnectionType:Connection = MongoConnection;

    constructor() {
        super();
    }

    public static connectEmitter(connection: MongoConnection): Promise<{ dbInstance: Db, client: MongoClient }> {
            const connectionConfig = {
                authSource: connection.authDB
            };

            return MongoClient.connect(connection.getConnectionString(), connectionConfig)
                .then((client: MongoClient) => {
                    return {client}
                });
        }
}
```

**Setting connectable model connection name**

By default connectable model use connection which label by name "default" \(case sensitive\).

For changing the connection name use:

1. Class static method `setConnectionName(name:string)`:

   ```text
    Post.setConnectionName("adminDB");
   ```

2. `@ConnectionName(name:string)` decorator:

   ```text
    @ConnectionName("adminDB")
    export class Post extends ModelAbstract{
    }
   ```


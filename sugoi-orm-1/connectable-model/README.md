---
description: Models that are based on direct connection to DB
---

# Connectable model

Example \(by the [@sugoi/mongodb](https://www.npmjs.com/package/@sugoi/mongodb) package implementation\):

```typescript
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

By default connectable models use connection which labeled by the name "default" \(case sensitive\).

For changing the connection name use:

1. Class static method `setConnectionName(name:string)`:

   ```typescript
    Post.setConnectionName("adminDB");
   ```

2. `@ConnectionName(name:string)` decorator:

   ```typescript
    @ConnectionName("adminDB")
    export class Post extends ModelAbstract{
    }
   ```


---
description: Models that are based on direct connection to DB
---

# Connectable model

Example \(by the @sugoi/mongodb package implementation\):

**First Step - Set connection item**

Connection item is the class which contains all of the communication establishing/closing logic. Another role of this class is to reflect the connection current status. This class must implement the IConnection interface!

```typescript
    import {CONNECTION_STATUS, IConnection} from "@sugoi/orm";
    import {Db, MongoClient} from "mongodb";
    import {IMongoConnectionConfig} from "../interfaces/mongo-connection-config.interface";


    export class MongoConnection implements IConnection, IMongoConnectionConfig {
        protocol: string = `mongodb://`;
        port: number = 27017;
        hostName: string;
        status: CONNECTION_STATUS;
        connectionClient: {
            dbInstance: Db,
            client: MongoClient
        };
        db?: string;
        connectionName?: string;
        user?: string;
        password?: string;
        authDB?: string;
        public newParser: boolean = false;


        connect(): Promise<boolean> {
            const connectionConfig = {
                authSource: this.authDB || this.db
            };
            if (this.user && this.password) {
                connectionConfig['auth'] = {
                    user: this.user,
                    password: this.password
                };
            }
            if (this.shouldUseNewParser()) {
                connectionConfig['useNewUrlParser'] = true;
            }

            return MongoClient.connect(this.getConnectionString(), connectionConfig)
                .then((client: MongoClient) => {
                    client.on("error", () => this.disconnect());
                    this.connectionClient = {
                        dbInstance: client.db(this.db),
                        client
                    };
                    return true
                })
                .catch(err => {
                    console.error(err);
                    throw err;
                });
        }


        isConnected(): Promise<boolean> {
            return Promise.resolve(this.status === CONNECTION_STATUS.CONNECTED);
        }


        public shouldUseNewParser(): boolean {
            return this.newParser;
        }

        public disconnect() {
            if (!this.connectionClient)
                return Promise.resolve(false);
            else {
                return this.connectionClient.client.close(true)
                    .then((disconnectObject) => {
                        this.status = CONNECTION_STATUS.DISCONNECTED
                        return true;
                    });
            }

        }

        public getConnectionString() {
            let connString = this.protocol;
            if (this.user && this.password) {
                connString += `${this.user}:${this.password}@`;
            }
            connString += `${this.hostName}:${this.port}`;
            return connString;
        }
    }

    MongoModel.setConnection({
        port: 27017,
        protocol: "mongodb://",
        hostName: "127.0.0.1",
        db: "SUGOIJS-EXAMPLE",
        newParser: true
    },MongoConnection,"SUGOIJS-EXAMPLE-CONNECTION")    
```

**Second Step - Setup the connection by config**

Setting a connection done by the ConnectableModel `setConnection` static function: `public static setConnection(configData: IConnectionConfig, connectionClass:, connectionName: string = "default"): Promise<IConnectionConfig>`

\`\`

This method will create a connection item and store it for later use. Also, the connect method will get called.


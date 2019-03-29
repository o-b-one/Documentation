---
description: Initialize Redis client
---

# Boostrapping



## Initialization

Initialization done by the static method `CreateConnection` of the `RedisProvider`

```typescript
static CreateConnection(connectionConfig: IRedisConfig, connectionName: string): TRedisProvider;
```

### **Basic**

```typescript
const redisProvider = RedisProvider.CreateConnection({
    host: "127.0.0.1",
    port: 6379,
    isDefault: true
});
const resolvedClient = RedisProvider.getConnection();
expect(redisProvider).toBe(resolvedClient); // Should be truthy
```

### Using [@sugoi/server](https://www.npmjs.com/package/@sugoi/server)

```typescript
@ServerModule({
    services: [
        {
            provide: RedisProvider.CreateConnection({
                             host: "127.0.0.1",
                             port: 6379,
                             isDefault: true
                      }),
            useName: "RedisService"
        }
    ]
})
export class BootstrapModule {
    constructor(@Inject('RedisService') private _redisService: TRedisProvider) {
    }
}
```


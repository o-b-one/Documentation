---
description: The Redis client handler class
---

# RedisProvider



The RedisProvider class instance re-exports all of redis methods with promise handler for callback.

All of the redis APIs remains the same as for [Node](https://github.com/NodeRedis/node_redis)Redis

#### Example

```typescript
await RedisProvider.GetConnection().set('test', '1');
await RedisProvider.GetConnection().get('test'); // Result will be '1'
```


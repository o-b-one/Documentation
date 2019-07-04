# Pub/Sub

## Publish

Publish done by redis client publish method

```typescript
publish(channel: string, value: string): Promise<number>;
```

### **Example**

```typescript
RedisProvider.GetConnection().publish("room-1", "data");
```

## Subscribe

The subscription done by a single method that returns an observable object of type PubSubMessage

```typescript
public getSubscriber<DataType>(byPattern: boolean, channelOrPattern: string): Observable<PubSubMessage<DataType>>
```

`PubSubMessage` class

```text
{
    hasError: boolean;
    data: any;
    error: any;
    type: "data"|"close"|"error"|"init";
    channel: string;
    pattern?: string; // Only in case of pattern subscribe
}
```

### **Example**

```typescript
RedisProvider.GetConnection().getSubscriber(true, "room-*").subscribe(
message=>{
    // handle message
},
err=>{
    // handle error
});
```

### **Decorators**

Another way to subscribe channel\pattern messages is using the following decorators

#### **Subscribe to channel**

```typescript
OnRedisMessage<ResponseType = any>(channel: string,...middlewares: Array<(msg: PubSubMessage<ResponseType>) => TValid>);
```

Or

```typescript
OnRedisMessage<ResponseType = any>(channel: string,connectionName?: string,...middlewares: Array<(msg: PubSubMessage<ResponseType>) => TValid>);
```

**Example:**

```typescript
 @OnRedisMessage('decoratorTest', (msg) => {
    return msg.data > 10; // This middleware will act as filter,
                          // only messagea with data greater than 10 will continue to the next method

    })
    public static channelListener(data) {
        this.decoratorTestChannel = data
    }
```

**Subscribe to pattern**

```text
OnRedisPMessage<ResponseType = any>(channel: string,...middlewares: Array<(msg: PubSubMessage<ResponseType>) => TValid>);
```

Or

```text
OnRedisPMessage<ResponseType = any>(channel: string,connectionName?: string,...middlewares: Array<(msg: PubSubMessage<ResponseType>) => TValid>);
```

**Example:**

```typescript
@OnRedisPMessage('decoratorTestPattern-*', null, (msg:PubSubMessage<number>) => {
    return msg.data > 10; // This middleware will act as filter,
                          // only messagea with data greater than 10 will continue to the next method
})
public static patternListener(msg) {
    this.decoratorTestPattern = msg;
}
```


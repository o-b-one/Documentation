# Upgrade to V4

## Upgrade existing project

Upgrade your project will take few moments using those steps:

```
$ npm i -g @sugoi/cli && npm i -D @sugoi/cli
```

{% hint style="info" %}
 Run those commands under you SugoiJS project
{% endhint %}

### Update server init

V4 change the signature of the server init method by removing the unused `serverMetaKey` argument. This cause the following change:

```typescript
HttpServer.init(BootstrapModule, "/", null, Authorization)
```

to 

```typescript
HttpServer.init(BootstrapModule, "/", Authorization)
```

Once commands are done you are ready to go by using the [build command](../sugoi-cli/commands.md#build):

```
$ sgi build
```




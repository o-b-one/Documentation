---
description: Setting up the web server
---

# Bootstrapping

## Bootstrapping

### Overview

To bootstrap your server use the `init` method:

```typescript
init(boostrapModule: any, rootPath?: string, authProvider?: AuthProvider,httpsConfiguration:any)
```

> bootstrapModule - the init module which use as entry point, contains references to other modules if needed.
>
> rootPath - Server uri prefix

> authProvider - the authorization services, more on that on Authorization section
>
> httpsConfiguration -  configuration for setting the connection as https \(mostly use for - {cert:certificatePath,key:keyPath}\)

### Simple usage

```typescript
import {HttpServer} from "@sugoi/server";

const server:HttpServer = HttpServer.init(BootstrapModule,"/api")
                                    .build()
                                    .listen(3000);
```

### Setting middlewares and Error handlers

For setting static file serving use:

```typescript
setStatic(pathToStatic:string,route?:string)
```

For setting middlewares use:

```typescript
setMiddlewares(...(app)=>void)
```

For setting error handlers use:

```typescript
setErrorHandlers((app) => void)
```

#### Predefined error handler

SugoiJS provides a predefined error handler named _\(defaultErrorHandler\)_ which provides loggin the error and returning an error to the customer.

Example:

```typescript
app.use(defaultErrorHandler(<boolean>isDev))
```

Full example:

```typescript
(<HttpServer>server)
    .setStatic("assets/admin","/admin")
    .setStatic("assets/main")
    .setMiddlewares((app) => {
        app.use(bodyParser.json());
        app.use(compression());
        if (DEVELOPMENT) {
            app.set('json spaces', 2);
            app.use(cors());
            app.use(require('morgan')('dev'));
        }
        app.use(express.static(paths.static));
    })
    .setErrorHandlers((app) => {
        app.use(function (req, res, next) {
            return res.sendFile(path.resolve(paths.index))
        });
        app.use(defaultErrorHandler(isDev));
    });
```

#### 

### Build & listen

After setting the middlewares and error handlers, build and listen to requests by:

```typescript
server.build()
    .listen(PORT, (error: Error) => {
        if (error) {
            logger.error(error.message);
            throw error;
        }
        logger.debug(`Server running @ ${HOST}:${PORT}`);
    });
```

This call will return http.Server instance which can be use for setting app variables, socket server and more.

### Full example

```typescript
server.setStatic("assets")
    .setMiddlewares((app) => {
        app.use(bodyParser.json());
        app.use(compression());
    })
    .setErrorHandlers((app) => {
        app.use(function (req, res, next) {
            return res.sendFile(path.resolve(paths.index))
        });
        app.use((req,res,next)=>{
            return function(err){
                if(err instanceof SugoiServerError){
                    console.log.error(err.stack);
                    console.log.error(`${err.message} ${JSON.stringify(err.data)});
                    res.status(500).send("Internal error");
                }
            }
        });
    });
```

## Retrieving the server app

For retrieving the server application use the HttpServer instance method `getServer()` , this method will return the common server application which will allow you to use `.get`,`.put`,`.use` etc..

### Example

```typescript
const httpServer = server.build();
const app = httpServer.getServer();
app.get("/",(req,res,next)=>{
    res.json({success:true,data:{}});
})

httpServer.listen(3000)
```

SugoiJS support migrate existing project by providing hybrid mode.

For achieving this approach use the `initializeFrom` method

`HttpServer.initializeFrom(sourceApp: TServer, bootstrapModule: any, authProvider?: TNewable<AuthProvider>)`

`TServer - http.Server | https.Server | { listen: (...args) => any }`

#### Example

```typescript
import {HttpServer} from "@sugoi/server";

const server:HttpServer = HttpServer.initializeFrom(myExpressApp,ServerModule);
```

### 


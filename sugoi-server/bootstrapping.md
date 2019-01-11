---
description: Setting up the web server
---

# Bootstrapping

### Bootstrapping

To boostrap you server use the `init` method:

```typescript
init(boostrapModule: any, rootPath?: string, moduleMetaKey?: string, authProvider?: AuthProvider)
```

> bootstrapModule - the init module which use as entry point, contains references to other modules if needed.
>
> rootPath - Server uri prefix
>
> moduleMetaKey\(optional - null by default\) - define the namespace of this server, this will help us to define which module belongs to which server instance. 
>
> authProvider - the authorization services, more on that on Authorization section

```text
import {HttpServer} from "@sugoi/server";

const server:HttpServer = HttpServer.init(BootstrapModule,"/api");
```

#### 

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


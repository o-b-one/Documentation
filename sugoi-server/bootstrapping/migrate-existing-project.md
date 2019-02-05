# Migrate existing project

## Overview

SugoiJS support migrate existing project by providing hybrid mode.

For achieving this approach you only need to use the `initializeFrom` method

`HttpServer.initializeFrom(sourceApp: TServer, bootstrapModule: any, authProvider?: TNewable<AuthProvider>)`

`TServer - http.Server | https.Server | { listen: (...args) => any }`

#### Example

```typescript
import {HttpServer} from "@sugoi/server";

const server:HttpServer = HttpServer.initializeFrom(myExpressApp,ServerModule);
server.build().listen(3000);
```

### 


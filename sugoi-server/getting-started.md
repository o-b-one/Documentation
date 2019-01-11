---
description: Setting up the web server
---

# Getting started

The SugoiJS server module provides express based web server, thanks to inversify-express-utils.

This module contain utils for singleton services, request handling decorators, request policies and authorization policies decorators. 

This module helps you define microservices by using module based architecture.

### Installation

> npm install --save @sugoi/server

#### tsconfig.json:

Under your tsconfig - compilerOptions set:

* `"target": "es5"`
* `"emitDecoratorMetadata": true`
* `"experimentalDecorators": true`
* `"lib": ["es2015","dom"]`

**Template**

You are able to use the config template which was set for the @sugoi/demo application:

```text
{
  "compilerOptions": {
    "baseUrl": "./src",
    "allowJs": true,
    "target": "es5",
    "module": "commonjs",
    "moduleResolution": "node",
    "sourceMap": true,
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "lib": [
      "es2015",
      "dom"
    ],
    "typeRoots": [
      "./node_modules/@types"
    ],
    "types": [
      "body-parser",
      "express",
      "node"
    ]
  }
}
```


---
description: Setting up the web server
---

# Getting started

[![npm version](https://badge.fury.io/js/%40sugoi%2Fserver.svg)](https://badge.fury.io/js/%40sugoi%2Fserver) [![Build Status](https://travis-ci.org/sugoiJS/server.svg?branch=master)](https://travis-ci.org/sugoiJS/server) [![codecov](https://codecov.io/gh/sugoiJS/server/branch/master/graph/badge.svg)](https://codecov.io/gh/sugoiJS/server)

The SugoiJS server module provides express based web server, thanks to inversify-express-utils.

This module contain utils for singleton services, request handling decorators, request policies and authorization policies decorators. 

This module helps you define microservices by using module based architecture.

### Installation

> npm install --save @sugoi/server

#### tsconfig.json:

Under your tsconfig - compilerOptions set:

* `"target": "es2015"`
* `"emitDecoratorMetadata": true`
* `"experimentalDecorators": true`
* `"lib": ["es2015","dom"]`

**Template**

You can use the config template that was set for the @sugoi/demo application:

```text
{
  "compilerOptions": {
    "baseUrl": "./src",
    "allowJs": true,
    "target": "es2015",
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


---
description: 'SugoiJS socket module, based on socket.io package'
---

# Getting started

[![npm version](https://badge.fury.io/js/%40sugoi%2Fsocket.svg)](https://badge.fury.io/js/%40sugoi%2Fsocket) [![Build Status](https://travis-ci.org/sugoiJS/socket.svg?branch=master)](https://travis-ci.org/sugoiJS/socket) [![codecov](https://codecov.io/gh/sugoiJS/socket/branch/master/graph/badge.svg)](https://codecov.io/gh/sugoiJS/socket)

## Installation

### @sugoi/cli

Check the [get started](../get-started.md) section!

### Manually

> npm install --save @sugoi/socket

#### tsconfig.json:

Under your tsconfig - compilerOptions set:

* `"target": "es2015"`
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


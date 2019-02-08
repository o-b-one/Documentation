# Getting started

[![npm version](https://badge.fury.io/js/%40sugoi%2Fredis.svg)](https://badge.fury.io/js/%40sugoi%2Fredis) [![Build Status](https://travis-ci.org/sugoiJS/redis.svg?branch=master)](https://travis-ci.org/sugoiJS/redis) [![codecov](https://codecov.io/gh/sugoiJS/redis/branch/master/graph/badge.svg)](https://codecov.io/gh/sugoiJS/redis)

## Installation

> npm install --save @sugoi/redis

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


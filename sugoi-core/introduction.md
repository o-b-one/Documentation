---
description: >-
  The core module of SugoiJS supplies the main classes and functions which are
  used by sugois' modules.
---

# Getting started

Some of the module features are:

* Extendable exception classes.
* Singleton objects & injections \(powered by [InversifyJS](https://github.com/inversify/inversifyjs)\).
* Policies - argument validator + decorator implementation.

### Installation

> npm install --save @sugoi/core

#### tsconfig.json:

Under your tsconfig - compilerOptions set:

* `"target": "es2015"`
* `"emitDecoratorMetadata": true`
* `"experimentalDecorators": true`
* `"lib": ["es2015","dom"]`

**Template**

You can use the config template which was set for the @sugoi/demo application:

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


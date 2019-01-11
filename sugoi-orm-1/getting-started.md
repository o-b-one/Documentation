---
description: The ORM module of SugoiJS provides all that need for CRUD action.
---

# Getting started

The ORM module of SugoiJS provides all that need for CRUD action by supply lifecycle driven mechanism, abstraction for encapsulated shared logic for CRUD and connection handling.

### Installation

> npm install --save @sugoi/orm

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


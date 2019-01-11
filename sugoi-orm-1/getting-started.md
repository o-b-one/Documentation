---
description: The ORM module of SugoiJS provides all that need for CRUD action.
---

# Getting started

[![npm version](https://badge.fury.io/js/%40sugoi%2Form.svg)](https://badge.fury.io/js/%40sugoi%2Form) [![Build Status](https://travis-ci.org/sugoiJS/ORM.svg?branch=master)](https://travis-ci.org/sugoiJS/ORM) [![codecov](https://codecov.io/gh/sugoiJS/ORM/branch/master/graph/badge.svg)](https://codecov.io/gh/sugoiJS/ORM)

The ORM module of SugoiJS provides all you need for CRUD actions by supplying lifecycle driven mechanism, abstraction for encapsulated shared logic for CRUD and connection handling.

### Installation

> npm install --save @sugoi/orm

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


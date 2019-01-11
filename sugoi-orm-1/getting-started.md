---
description: The ORM module of SugoiJS provides all that need for CRUD action.
---

# Getting started

[![npm version](https://badge.fury.io/js/%40sugoi%2Form.svg)](https://badge.fury.io/js/%40sugoi%2Form) [![Build Status](https://travis-ci.org/sugoiJS/ORM.svg?branch=master)](https://travis-ci.org/sugoiJS/ORM) [![codecov](https://codecov.io/gh/sugoiJS/ORM/branch/master/graph/badge.svg)](https://codecov.io/gh/sugoiJS/ORM)

## Overview

The ORM module of SugoiJS provides all you need for defining models with CRUD actions. This done by supplying lifecycle driven mechanism, abstraction and connection handling.

The ORM module designed to give you the flexability of defining your CRUD logic along with encapsulation of complex lifecycle mechanism.

## Installation

### @sugoi/cli

Check the [get started](../get-started.md) section!

### Manually

> npm install --save @sugoi/orm

#### tsconfig.json:

Under your tsconfig - compilerOptions set:

* `"target": "es2015"`
* `"emitDecoratorMetadata": true`
* `"experimentalDecorators": true`
* `"lib": ["es2015","dom"]`

#### **Template**

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


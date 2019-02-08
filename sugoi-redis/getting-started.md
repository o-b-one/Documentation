# Getting started



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


---
description: Environment based configuration
---

# Configurations

## Overview

Since V4 of SugoiJS, it's allowed to define properties as part of the configuration of application.

The configuration directory  found on the root level of the server directory, in the following structure:

* root
  * server
    * configuration
      * default
        * security.js
        * ssl.js
        * variables.js
      * &lt;environment&gt;
        * security.js
        * ssl.js
        * variables.js

## Configuration files

### security.js

Powered by [HelmetJS](https://www.npmjs.com/package/helmet). Provides basic security layer to you web server.

#### Configuration

```javascript
{
    enabled: true,
    options:  undefined // use helmetjs default configuration, can be replace by:

    // more info: https://helmetjs.github.io/docs
    // {
    //     contentSecurityPolicy: {
    //         directives: {
    //             defaultSrc: ["'self'"],
    //             styleSrc: ["'self'", 'maxcdn.bootstrapcdn.com']
    //           }
    //     },
    //     dnsPrefetchControl: true,
    //     frameguard: true,
    //     hidePoweredBy: true,
    //     hpkp: {
    //         maxAge: 7776000,
    //         sha256s: ['AbCdEf123=', 'ZyXwVu456=']
    //     },
    //     hsts: true,
    //     ieNoOpen: true,
    //     noCache: false,
    //     noSniff: true,
    //     xssFilter: true,
    //     expectCt: true
    //  }
}
```

#### ssl.js

Define the path to the ssl certificate  files

#### Configuration

```javascript
const path = require('path');

module.exports = null // can be replaced with:
{
    cert: path.resolve('pathToCertFile'),
    key: path.resolve('pathToKeyFile')
}
```

### variables.js

Map of environment variables to inject in build time.

access to those environment variable is possible with  Configuration resolve.



### Many others...

{% hint style="info" %}
### Feel free to add your files which their content will be added to the configuration map that available in run-time.
{% endhint %}




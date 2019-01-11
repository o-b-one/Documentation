---
description: >-
  SugoiJS - A minimal modular framework,which gives you the ability to use only
  what you need, fast.
---

# What is SugoiJS?

SugoiJS is a modular framework which gives you the ability to develop faster by using just what you need.

SugoiJS decrease the amount of boilerplates in your code while using abstraction and decorator syntax, by using the OOP SOLID principles. 

More then that, SugoiJS provide lifecycle driven flow, for easier flow define in your application. This will also help to get easier debugging and testing process.

The combination of TypeScript, decorators, abstraction and predefined lifecycles will optimize your development experience along with your application reliability.



SugoiJS has 4 root modules which acts as standalone units:

* \*\*\*\*[**@sugoi/core**](https://github.com/sugoiJS/Core) - This is the core module of SugoiJS, it define reusable components like policies\(aka Guards\), extendable exceptions, container handler \(for singleton\), service injection and many more.
* \*\*\*\*[**@sugoi/orm**](https://sugoijs.com/#/documentation/orm/index) - The ORM module use for o[bject-relational](https://en.wikipedia.org/wiki/Object-relational_mapping) mapping. this module define abstract models for REST use and DB connection use. along with casting resources to TypeScript objects the ORM module provide CRUD + lifecycle flow \(before\(CRUD\),after\(CRUD\), beforeValidate,validate\). - Sub-module of this module is [@sugoi\mongodb](https://sugoijs.com/#/documentation/mongoDB/index).
* \*\*\*\*[**@sugoi/server**](https://sugoijs.com/#/documentation/server/index) - The server module provide fully decorated, [express ](https://github.com/expressjs)based web server with additional abilities like:

  * Service injection.
  * Request validators \(params, body, query params, headers\).
  * Authorization and roles validators.

  and many more.

* [**@sugoi/socket**](https://sugoijs.com/#/documentation/sockets/index) - The socket module is easy plug and play socket handler module which based on [socket.io](https://github.com/socketio/socket.io). This module give you the ability to bind event to function using the @SocketOn\(eventName\) decorator on top of the function.

Try it now with our [demo application](http://demo.sugoijs.com/)


---
description: >-
  SugoiJS - A minimal modular framework which gives you the ability to use only
  what you need, fast.
---

# What is SugoiJS?

SugoiJS is a modular framework which gives you the ability to develop faster while using just what you need.

SugoiJS decreases the amount of boilerplates in your code while using abstraction and decorator syntax and implementing the OOP SOLID principles. 

In addition, SugoiJS provides an easier definition of fows in your application with predefined lifecycle hooks. It helps you to get easier debugging and testing process.

The combination of TypeScript, decorators, abstractions and predefined lifecycles will optimize your development experience along with your application reliability.

SugoiJS has four root modules that act as standalone units:

* \*\*\*\*[**@sugoi/core**](https://github.com/sugoiJS/Core) - This is the core module of SugoiJS, it defines reusable components like policies \(aka Guards\), extendable exceptions, container handler \(for singleton\), service injection and much more...
* \*\*\*\*[**@sugoi/orm**](https://sugoijs.com/#/documentation/orm/index) - The ORM module is used for o[bject-relational](https://en.wikipedia.org/wiki/Object-relational_mapping) mapping. this module defines abstract models for REST usage and DB connection usage. As well as casting resources to class instances, the ORM module provides CRUD and lifecycle flow:  before\(CRUD\),after\(CRUD\), beforeValidate,validate. - Sub-module of this module is [@sugoi\mongodb](https://sugoijs.com/#/documentation/mongoDB/index).
* \*\*\*\*[**@sugoi/server**](https://sugoijs.com/#/documentation/server/index) - The server module provides fully decorated [express ](https://github.com/expressjs)based web server with additional abilities like:

  * Service injection.
  * Request validators \(params, body, query params, headers\).
  * Authorization and roles validators.

  and much more...

* [**@sugoi/socket**](https://sugoijs.com/#/documentation/sockets/index) - The socket module is an easy plug and play socket handler module which based on [socket.io](https://github.com/socketio/socket.io). This module gives you the ability to bind event to function using the @SocketOn\(eventName\) decorator on top of the function.

Try it now with our [demo application](http://demo.sugoijs.com/)


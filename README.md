---
description: '"Sugoi" - Awesome in Japanese. As the development process should be.'
---

# What is SugoiJS?

SugoiJS - A minimal modular framework,which gives you the ability to use only what you need, fast.

SugoiJS is a modular framework which gives you the ability to develop faster while using just what you need.

SugoiJS decreases the amount of boilerplate code while using abstraction and decorators syntax while using OOP and SOLID principles. 

SugoiJS provides an easier definition of fows in your application with predefined lifecycle hooks. It helps you to get easier debugging and testing process.

The combination of TypeScript, decorators, abstractions and predefined lifecycles will optimize your development experience along with your application reliability.

SugoiJS has four root modules that act as standalone units:

* \*\*\*\*[**@sugoi/core**](https://wiki.sugoijs.com/sugoi-core/introduction) - This is the core module of SugoiJS, it defines reusable components like policies \(aka Guards\), extendable exceptions, container handler \(for singleton\), service injection and much more! \*The core module is imported and used by all of the SugoiJS modules.
* \*\*\*\*[**@sugoi/server**](https://wiki.sugoijs.com/sugoi-server/getting-started) - The server module provides fully decorated [express ](https://github.com/expressjs)based web server with additional abilities like:

  * Service injection.
  * Request validators \(params, body, query params, headers\).
  * Authorization and roles validators.

  and much more!

* \*\*\*\*[**@sugoi/orm**](https://wiki.sugoijs.com/sugoi-orm-1/getting-started) - The ORM module is used for o[bject-relational](https://en.wikipedia.org/wiki/Object-relational_mapping) mapping. this module defines abstract models for REST usage and DB connection usage. As well as casting resources to class instances, the ORM module provides CRUD and lifecycle flow:  before\(CRUD\),after\(CRUD\), beforeValidate,validate. - Sub-module of this module is [@sugoi\mongodb](https://sugoijs.com/#/documentation/mongoDB/index).
* [**@sugoi/socket**](https://wiki.sugoijs.com/sugoi-socket/getting-started) - The socket module is an easy plug and play socket handler module which based on [socket.io](https://github.com/socketio/socket.io). This module gives you the ability to bind event to function using the @SocketOn\(eventName\) decorator on top of the function.

Try it now with our [demo application](http://demo.sugoijs.com/)


---
description: The SugoiJS cli pre-defined commands
---

# Commands

## Initialization

For  initiating a new project use the `init` command.

```bash
$ sgi init
```

After you'll run this command you will need to answer few questions which will help you to set the application you need

## Generate

SugoiJS provides easy generation tool by the `g` or `generate` argument

```bash
$ sgi g <type> <name>
```

### Available types

* **module \(m\)** - Generate a module with one service and one controller which contains the module name 
  * After generating new module you will have to inject it to bootstrap module.
* **controller \(c\)** - Generate a controller under 'controllers' directory.
  * After generating new controller you will have to inject it to the related module.
* **service \(s\)** - Generate a service under 'services' directory.
  * After generating new service you will have to inject it to the related module.
* **model** - Generate a model class.
* **mongo-model** - Generate a mongo model class.

### Commands example

```bash
$ sgi g m myModule
// Will create a module under the current path 
// with controller and a service
```

```bash
$ sgi g model myModel
// Will create a model under the current path 
```

```text
$ sgi g mongo-model myMongoModel
// Will create a mongo-model under the current path 
```

```bash
$ sgi g c newController
// Will create a controller under the current path 
// will create controllers directory 
// if no such directory found under the path
```

```bash
$ sgi g s newService
// Will create a service under the current path 
// will create service directory 
// if no such directory found under the path
```

### Build

SugoiJS provides easy build tool by the `build` argument.

```bash
$ sgi build
```

By default the environment which will be used for configuration is the "default" environment

{% hint style="info" %}
The SugoiJS build action requires the _sugoi.json_ file,  if it is missing on your project please execute update.

$ sgi update
{% endhint %}



#### Set build environment

For defining the environment to use in the build execute:

```bash
$ sgi build --environment=<enviroment>
```

For example:

```bash
$ sgi build --environment=production
```

### Update

For updating your project run and create missing files, execute:

```bash
$ sgi update
```

### Testing

SugoiJS using jest as testing infrastructure. 

For run those tests execute:

```bash
$ sgi test
```

 

{% hint style="info" %}
The SugoiJS test action requires the _jest.configuration.js_ file, if it is missing on your project please execute update.

$ sgi update
{% endhint %}


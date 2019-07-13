---
description: Server hooks to handle Pre and Post requests
---

# Hooks

## Overview

Hooks allows us to handle request based on the request method and URI pattern.

## Types

There are two types of hooks - Before and After, each type will apply first or last in order based on the type.

### BeforeHook

The before hook will apply first, before any middleware will take place

### AfterHook

The after hook will apply last, after the request ends and response returned to the client.

## Usage

### Basic usage

The Before and After hooks use as decorator for method

```typescript
    @BeforeHook(pattern: string, method?: HTTP_METHOD,  options?: IHookOptions)
    beforeHookFn(req, res, next) {
        // method to be apply before the endpoint trigger
    }
    
    
    @AfterHook(pattern: string, method?: HTTP_METHOD,  options?: IHookOptions)
    afterHookFn(req, res, next) {
        // method to be apply after the endpoint trigger
    }
```

{% hint style="info" %}
Hook should be end by calling to the `next` method
{% endhint %}

#### Example

```typescript
export class Hooks{
    static counter: number = 0
    
    private logger: Logger;
    @BeforeHook('*')
    beforeAll(req, res, next) {
        res.counter = ++Hooks.counter
        next()
    }

    @AfterHook('/*/:id', HTTP_METHOD.GET)
    afterRead(req, res, next) {
        const payload = Object.assign({reqCounter: req['counter']}, req.params)
        this.logger.log('read was apply', payload)
        next()
    }
}
```

### Priority

We can control the order of hooks apply be setting the hook priority.

{% hint style="info" %}
Lower the number is, hook priority is higher and will apply earlier
{% endhint %}

#### Example

```typescript
export class Hooks{
    static counter: number = 0
    
    private logger: Logger;
    @BeforeHook('*', HTTP_METHOD.ALL, {priority: 0}) // apply first
    beforeAll(req, res, next) {
        res.counter = ++Hooks.counter
        next()
    }

    @BeforeHook('/*/:id', HTTP_METHOD.GET, {priority: 1})// apply second
    beforeRead(req, res, next) {
        const payload = Object.assign({reqCounter: req['counter']}, req.params)
        this.logger.log('read was apply', payload)
        next()
    }
}
```


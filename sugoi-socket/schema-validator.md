---
description: Validating socket data made easy
---

# Schema validator

## Overview

SugoiJS provides easy, one line solution to validating the socket event payload using `@SocketSchemaPolicy` decorator.

The `SocketSchemaPolicy` is similar to server module `RequestSchemaPolicy` method.

## How it works

Schema policy wrap the method with the SugoiJS core module `ValidateSchemaUtil.validateArgs`  function.  
This function validate the payload using `ComparableSchema` object.  
In case the payload not fit the schema exception will thrown with details about the validation error.

## Usage

For using the socket payload schema validator all you need to do is to add single line after the `@SocketOn\@ServerOn` decorators

### Example

```typescript
@SocketOn("SEND_MESSAGE")
@SocketSchemaPolicy(ComparableSchema.ofType(SchemaTypes.STRING))
registerForClientUsage(socket, msg) {
    SocketHandler.getServer().emit("NEW_MESSAGE",{msg})
}
```

In that case we to validate the `msg` is indeed of type string, otherwise the function shouldn't apply.


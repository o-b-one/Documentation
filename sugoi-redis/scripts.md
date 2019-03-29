---
description: Apply lua scripts on redis server
---

# Scripts

## Overview

Running lua scripts can be done using the `runScripts` method

```text
runScripts(...scripts: Array<ScriptResource>): Promise<any>
```

The `ScriptResource` provides an API for loading inline scripts and file scripts

## Inline scripts

Using the `ofScript` method allows us to create a script from inline text

### **Example:**

```typescript
const inlineScriptResource = ScriptResource.OfScript('return redis.call("HSET",KEYS[1],ARGV[1],ARGV[2])')
                                            .setKeys('myKey')
                                            .setArgs('FIELD', 'myValue');
await RedisProvider.GetConnection().runScripts(inlineScriptResource);
```

## File scripts

Using the `ofFile` method allows us to create a script from inline text

### **Example:**

```typescript
const fileScriptResource = OfFile(__dirname + '/lua-scripts/myScript.lua')
                                            .setKeys('myKey')
                                            .setArgs('FIELD', 'myValue');
await RedisProvider.GetConnection().runScripts(fileScriptResource);
```


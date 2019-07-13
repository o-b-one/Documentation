---
description: Setting request timeout with minimum effort
---

# Timeout

## Overview

SugoiJS provides an easy way to set the timeout for a request based on the endpoint using the `@Timeout` decorator.

## @Timeout decorator

Using the `@Timeout` decorator we can set a timeout on a method and define a callback in case of a timeout.

`Timeout(ms: number, onTimeout?: (req, res) => void)`

#### Example

```typescript
export class TimeoutMethod{
    @HttpGet('/timeout')
    @Timeout(1000, (request, response) => {
        console.error("timeout called")
        response.json({timeout: true})
    })
    public async timeout() {
        return await new Promise(resolve => {
            setTimeout(() => {
                resolve({data: new Date()})
            }, 2000)
    }
}
```


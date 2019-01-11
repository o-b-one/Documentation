---
description: Handling server response with custom and pre-define responses
---

# Response handling

## Response handling

The response handling done by resolving object, this will trigger the default response handler which return the resolved object with status code 200 and `content-type` of `application\json` for setting your own responses you can use the `HttpResponse` class.

### HttpResponse

This class equipped with builder and helper function with set to give you the ability to set the response content, status code and headers.

#### Usage example



```typescript
@HttpGet("/")
public async example() {
    return HttpResponse.builder(message)
        .setHeaders({"Cache-Control": "max-age=120"})
        .setStatusCode(202);
}
```

#### Shorthand

```typescript
@HttpGet("/")
public async example() {
    return HttpResponse.builder(message,{"Cache-Control": "max-age=120"},202);
}
```

### Pre-defined responses

* Forbidden
* NotFound
* Ok
* ServerError
* Unauthorized
* BadRequest

#### Usage example



```typescript
@Controller("/")
export class Responses{
    @HttpGet("/notfound")
    async notFound() {
        return NotFound("not found");
    }
    
    @HttpGet("/servererror")
    async serverError() {
        return ServerError("error");
    }
    
    @HttpGet("/unauthorized")
    async unauthorized() {
        return Unauthorized("unauthorized");
    }
    
    @HttpGet("/forbidden")
    async forbidden() {
        return Forbidden("forbidden");
    }
    
    @HttpGet("/ok")
    async ok() {
        return Ok("ok");
    }
    
    @HttpGet("/badrequest")
    async badrequest() {
        return BadRequest("bad request");
    }
}
```


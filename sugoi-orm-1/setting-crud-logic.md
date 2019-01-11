---
description: The ModelAbstract define the interface all is left is to set the logic behind
---

# Setting CRUD logic

For CRUD support, you need to implement your CRUD logic under each of the CRUD emitters:

**1. saveEmitter**

```text
public saveEmitter(options?:QueryOptions): Promise<any> {
        return rp({
            method: 'POST',
            uri: 'https://api.example.com/myendpoint',
            body:this,
            json: true
        })
}
```

**2. findEmitter \(static\)**

```text
protected static findEmitter(query: any, options?:QueryOptions): Promise<any> {
        return rp({
            method: 'GET',
            uri: 'https://api.example.com/myendpoint',
            qs:query,
            json: true
        })
}
```

**3. updateEmitter**

```text
public updateEmitter(options?:QueryOptions): Promise<any> {
        return rp({
            method: 'PUT',
            uri: `https://api.example.com/myendpoint/${this.id}`,
            body:this,
            json: true
        })
}
```

**4. removeEmitter \(static\)**

```text
protected static removeEmitter(query?,options?:QueryOptions):Promise<any> {
        return rp({
            method: 'DELETE',
            uri: `https://api.example.com/myendpoint/${query.id}`,
            body: this,
            json: true
        })
}
```


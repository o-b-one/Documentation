---
description: >-
  The Model Abstract defines the interface. All that is left for you is to set
  the logic behind.
---

# Setting CRUD logic

## Overview

SugoiJS provides custom CRUD actions for models using the CRUD emitter.

## Initialize 

For CRUD support, you need to implement your CRUD logic under each of the CRUD emitters.

### **saveEmitter**

```typescript
public saveEmitter(options?:QueryOptions,data?:any): Promise<any> {
        return rp({
            method: 'POST',
            uri: 'https://api.example.com/myendpoint',
            body: data,
            json: true
        })
}
```

### **findEmitter \(static\)**

```typescript
protected static findEmitter(query: any, options?:QueryOptions): Promise<any> {
        return rp({
            method: 'GET',
            uri: 'https://api.example.com/myendpoint',
            qs:query,
            json: true
        })
}
```

### **updateEmitter**

```typescript
public updateEmitter(options?:QueryOptions,data:any): Promise<any> {
        return rp({
            method: 'PUT',
            uri: `https://api.example.com/myendpoint/${this.id}`,
            body: data,
            json: true
        })
}
```

### **removeEmitter \(static\)**

```typescript
protected static removeEmitter(query?,options?:QueryOptions):Promise<any> {
        return rp({
            method: 'DELETE',
            uri: `https://api.example.com/myendpoint/${query.id}`,
            body: this,
            json: true
        })
}
```


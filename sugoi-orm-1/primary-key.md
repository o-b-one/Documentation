---
description: Define what is the right property to relay on for "_ById" queries
---

# Primary key

For query and upsert data SugoiJS use primary key of the instance\query object.

The primary key is a property which decorated with @Primary\(\)

Using the Primary key will be done by:

1. \(Utility function\) `getPrimaryKey(classToUse)`

   Return the primary key name from given class, if not found 'null' will be returned.

2. \(Static method\) `castIdToQuery(id:string,classToUse = this)`

   Will return an object with property name which is decorated with Primary as the key and the ID as the value

   `classToUse` - class to get the primary key from \(default is `this`\)

3. \(static method\) `getIdFromQuery(query: any,classToUse = this, deleteProperty:boolean = true)`

   If query contains the primary key the function will return the query primary key value.

   `classToUse` - class to get the primary key from \(default is `this`\).

   `deleteProperty` - delete primary key property from the query \(default is `true`\).

4. \(instance method\) `getIdQuery():{[prop:string]:string}`

   Returns a key value object of primary key and its' value for the current instance.

   if no primary key set the function will throw an exception;

Full example:

```typescript
export class Post extends ModelAbstract{
    @Primary()
    public postId:string = "post-12";

    public static getPostById(id:string): Promise<Post>{
        return this.find(this.castIdToQuery(id));
    }

    public getCurrentPost(): Promise<Post>{
        const query = getIdQuery(); // query = {postId:"post-12"}
        return Post.find(query);
    }

    public getPrimaryKeyName(): string{
        return getPrimaryKey(this);// result is "postId"
    }

}
```

All of the @sugoi/orm predefined methods which is mentioned before using the primary key value.


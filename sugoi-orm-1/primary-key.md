---
description: Define what is the right property to relay on for "_ById" queries
---

# Primary key

For query and upsert data @sugoi use primary key of the instance\query object.

This primary key is property which decorated with @Primary\(\)

Using the Primary key will done by:

1. \(Utility function\) `getPrimaryKey(classToUse)`

   Return the primary key name from given class, if not found null will return.

2. \(static method\) `castIdToQuery(id:string,classToUse = this)`

   Will return an object with property name which decorate with Primary as key and the id as value

   `classToUse` - class to get the primary key from \(default is `this`\)

3. \(static method\) `getIdFromQuery(query: any,classToUse = this, deleteProperty:boolean = true)`

   If query contain the primary key the function will return the query primary key value.

   `classToUse` - class to get the primary key from \(default is `this`\)

   `deleteProperty` - delete primary key property from the query \(default is `true`\)

4. \(instance method\) `getIdQuery():{[prop:string]:string}`

   Return key value object of primary key and its value of the current instance

   if no primary key set the function will return null;

Full example:

```text
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

All of the @sugoi/orm predefined interface methods which mentioned before use the primary key value.


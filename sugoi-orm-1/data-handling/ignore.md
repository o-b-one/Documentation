---
description: 'Hiding fields from storing, serialization and response'
---

# Ignore fields

## @Ignore\(\)

Fields which decorate with `@Ignore()` will not be present during the storage procedure, response to client and serialization \( `JSON.stringify()` \).

Example:

```typescript
export class YourModel extends ModelAbstract{
    public id:string;
    public name:string;
    
    @Ignore()
    public shouldGenerateId:boolean;
    
    protected saveEmitter(options?: any): Promise<any> {
        if(this.shouldGenerateId){
            this.id = StringUtils.generateId();
        }    
        return rp({
            method: 'POST',
            uri: `/${this.getModelName()}`,
            body: JSON.stringify(this) // Won't contain `shouldGenerateId` property
        })
        
    }
}
```

### showIgnoredFields\(\) 

By default, all ignored fields won't present during serialization and response, you can toggle this logic off by calling `showIgnoredFields()` instance function.

### hideIgnoredFields\(\)  

The `hideIgnoredFields()`instance function will hide all of the fields which decorated with `Ignored()`.


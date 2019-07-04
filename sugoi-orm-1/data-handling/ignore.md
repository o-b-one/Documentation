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

### addFieldsToIgnore\(...fields:string\[\]\)

The `addFieldsToIgnore` instance function allow you to apply the ignore functionality without decorators, each field added to "ignored" will automatically be hidden.

### removeFieldsFromIgnored\(...fields:string\[\]\)

The `removeFieldsFromIgnore` instance function allow you to prohibit hiding fields using `hideIgnoredFields()` .  
The passed fields names can be either a field that decorated with `Ignore()` or fields which add with `addFieldsToIgnore()`. 

### hideIgnoredFields\(\)  

The `hideIgnoredFields()`instance function will hide all of the fields which decorated with `Ignored()` or added by `addFieldsToIgnore`.

### showIgnoredFields\(\) 

By default, all ignored fields won't present during serialization and response, you can toggle this logic off by calling `showIgnoredFields()` instance function.


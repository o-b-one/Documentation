---
description: Ready to use policies
---

# Pre-defined polices

## Function argument validation

@sugoi\core comes with pre-defined policy for validating functions arguments:

```typescript
ValidateSchemaPolicy(failedResponseCode: number = 400, ...policyMeta: TValidateSchemaMeta[])
```

> failedResponseCode: number - The code will be stored under the exception if the value does not meet the criteria.

> policyMeta: TValidateSchemaMeta - Meta data for validation.

```typescript
{
    schema: {[prop:string]:ComparableSchema}|ComparableSchema,
    argIndex?: number, - The argument index which need to validate - default is 0
    keyInArg?: string  - Key in argument (optional)
}
```

### Example: 

#### Schema -

```typescript
{
    role:{
        text:string//with regex  /([A-Z])+/i
    }
}
```

#### Usage -

```typescript
@ValidateSchemaPolicy(400, {
        schema: {
            "role": ComparableSchema.ofType(
                {text: ComparableSchema.ofType(SchemaTypes.STRING).setRegex("([A-Z])+", "i")}
            )
        },
        argIndex: 0
    })
```

### Result:

In case the argument doesn't meet the criteria an exception will thrown with the given failed response code


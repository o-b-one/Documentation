---
description: Model validation done right
---

# Validation and Required fields

## Validation in the lifecycle

if we will take a look again on the update\save lifecycle we will  be able to see validation is the 2nd step which occurs.

![SugoiJS save and update lifecycle hooks](../../.gitbook/assets/lifecycle.png)



## Handling model validation

### 1. validate\(\) function \(IValidate interface\)

If `validate` function is declared for the model it will get called, the response should be `Promise` of `true` or any other value, while `true` approve the model is valid.

Interface:  
`validate():Promise<true|any>`

### 2. @Required\(\) decorator

If property is decorate with `@Required()` it will be checked during the validation process.  


By default `@Required` check the value of the property isn't `null` or empty string.

#### `@Required(allowEmptyString:boolean)` 

For allowing empty strings pass the value `true` as argument, this will set the `allowEmptyString` argument.  
For disallow empty string pass `false`\(default\).

For example

```typescript
@Required(true)
public body:string;
```

#### @Required\(condition: ComparableValueType\)

For defining the property schema you able to pass `ComparableValueType`  as property.

For example:

```typescript
@Required({
    text:Comparable.ofType(SchemaTypes.STRING),
    body:Comparable.ofType(SchemaTypes.STRING),
})
public post;


```

## Required API

#### Get all required fields:

```typescript
public getMandatoryFields()
```

#### Get instance required fields:

#### 

```typescript
public getInstanceMandatoryFields()
```

#### Add field to required fields:

```typescript
public addMandatoryField(field: string, condition?: TComparableSchema);
public addMandatoryField(field: string, allowEmptyString?: boolean);
public addMandatoryField(field: string, condition?: boolean | TComparableSchema)
```

#### Remove field from required fields:



```typescript
public removeMandatoryFields(...fields:string[])
```

### Toggling required fields validation

For toggle the required fields validation on and off you can use:

#### Instance method 

```typescript
public skipRequiredFieldsValidation(shouldSkip: boolean):void
```

#### Query options

```typescript
QueryOptions.builder().setSkipRequiredValidation(true)
```

This option later will be use for the query:

```typescript
await User.updateById(id,{name:"testing"},QueryOptions.builder().setSkipRequiredValidation(true));
```


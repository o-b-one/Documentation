---
description: SugoiJS provides policy which can be use for guarding any function.
---

# Policies

Policies gives you the ability to apply argument check on a function with zero effort.

SugoiJS provides policy which can be use for guarding any function.

The Policies use by two simple steps:

**@Policy\(policyId?:string\)**

This decorator register the function as policy validator, which will later be used as guardian policy.

> policyId?: string - The id which will be use as an alias for calling this function, default is ${class name}.${function name}

**@UsePolicy\(policy: TPolicy\|string, failedResponseCode: number = 400, ...policyMeta: any\[\]\)**

This decorator set a policy guard on the function it decorated.

> policy:TPolicy\| string - For setting the refereed policy, use the policy Id from previous section nor anonymous function reference.
>
> failedResponseCode: number - The code which will be under the exception in case the value does not meet the criterias.
>
> policyMeta: any\[\] - Any further payload data which should pass to the policy.

#### Pre-defined policies:

@sugoi\core provide pre-defined policy for validating function arguments:

```text
ValidateSchemaPolicy(failedResponseCode: number = 400, ...policyMeta: TValidateSchemaMeta[])
```

> failedResponseCode: number - The code which will be under the exception in case the value does not meet the criterias.
>
> policyMeta: TValidateSchemaMeta - Meta data for validation

```text
{
    schema: {[prop:string]:ComparableSchema|ComparableSchema}, - Comperable schema
    argIndex?: number, - Function argument index - default is 0
    keyInArg?: string  - Key in argument
}
```

Example: Schema -

```text
{
    role:{
        text:string//with regex  /([A-Z])+/i
    }
}
```

Usage -

```text
@ValidateSchemaPolicy(400, {
        schema: {
            "role": ComparableSchema.ofType(
                {text: ComparableSchema.ofType(SchemaTypes.STRING).setRegex("([A-Z])+", "i")}
            )
        },
        argIndex: 0
    })
```

#### Build your own policies:

Policy can be any function of type TPolicy

> TPolicy = \(policyData?:{functionArgs: any\[\], policyMeta: any\[\]}\)=&gt;\(Promise &lt; \(true\|any\) &gt; \| \(true\|any\)\)

When result is boolean `true` means the data is valid, all the other values will be shown on the exception

#### Policy full example:

```text
class Validators{

    @Policy() //register this function as policy using the class name and function name, same as use @Policy("Validators.myNumberValidation")
    static myNumberValidation(policyData:{functionArgs: any[], policyMeta: {argIndexToValidate:number,maxValue:number}[]}): true|any{
        const myMeta = policyMeta[0];
        //those are the meta data values which passed to the decorator itself while using @UsePolicy()
        const argIndexToValidate = myMeta.argIndexToValidate;
        const maxValue = myMeta.maxValue;

        if(policyData.functionArgs[argIndexToValidate] < maxValue){
            return true; //Is valid, continue to the function/next policy
        }else{
            return policyData.functionArgs[argToValidate]; //so we will be able to identify the issue on the exception
        }
    }
}

@UsePolicy("Validators.myNumberValidation",{argIndexToValidate:0,maxValue:5})
lowerThan5NumberLogger(myNumber){
    console.log(`number is lower the 5! ${myNumber}`);
}
```


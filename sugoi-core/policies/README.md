---
description: SugoiJS provides policy that can be used for guarding any function.
---

# Policies \(Filters\)

## Guard your methods

Policies gives you the ability to apply arguments check on a function with zero effort.

SugoiJS provides policy which can be use for guarding any method.

The Policies are used by two simple steps:

### **Decorate your verification method with - @Policy\(policyId?:string\)**

This decorator registers the function as "policy validator", this will later be used as guardian middleware.

> policyId?: string - This ID will be used as an alias for calling this function, default is ${class name}.${function name}

#### Example



```typescript
 @Policy() //register this function as policy using the class name and function name, same as use @Policy("myNumberValidation")
    static myNumberValidation(
    policyData:{functionArgs: any[], 
    policyMeta: Array<{argIndexToValidate:number,maxValue:number}>
    }): true|any{

        // Those are the meta data values 
        // which passed into the decorator itself while using @UsePolicy()
        const argIndexToValidate = policyMeta[0].argIndexToValidate;
        const maxValue = policyMeta[0].maxValue;

        if(policyData.functionArgs[argIndexToValidate] < maxValue){
            return true; //Is valid, continue to the function/next policy or middleware
        }else{
            return policyData.functionArgs[argToValidate]; // so we will be able to identify the issue on the exception
        }
    }
```

**2. @UsePolicy\(policy: TPolicy\|string, failedResponseCode: number = 400, ...policyMeta: any\[\]\)**

This decorator sets a policy guard on the function it decorates:

> policy:TPolicy\| string - For setting the referenced policy, use the policy ID from the previous section or anonymous function reference.
>
> failedResponseCode: number - The code will be stored under the exception if the value does not meet the criteria.
>
> policyMeta: any\[\] - Any further payload data which should pass to the policy.

```typescript

/**
* Apply policy by anonymous function
* only numbers lower than 5 will log
**/
@UsePolicy((myNumber: number)=> myNumber < 5)
lowerThan5NumberLogger(myNumber){
    console.log(`number is lower the 5! ${myNumber}`);
}
```

#### Build your own policies:

Policy can be any function of type TPolicy

> TPolicy = \(policyData?:{functionArgs: any\[\], policyMeta: any\[\]}\)=&gt;\(Promise &lt; \(true\|any\) &gt; \| \(true\|any\)\)

When the result is boolean, `true` means that the data is valid, all other values will be shown on the exception

#### Policy full example:

```typescript
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


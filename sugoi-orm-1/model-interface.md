# Model interface

**Find**

> **\(static method\)** findAll\(query: any = {}, options?: QueryOptions\) - query all records
>
> **\(static method\)** findOne\(query: any = {}, options:QueryOptions ={limit:1}\) - query one record
>
> **\(static method\)** findById\(id: string \| number, options:QueryOptions ={limit:1}\) - query by id
>
> **\(static method\)** find\(query: any = {}, options?: QueryOptions\) - customize query

**Remove**

> **\(static method\)** removeAll\(query: any = {}, options?: QueryOptions\) - remove all records
>
> **\(static method\)** removeOne\(query: any = {}, options:QueryOptions ={limit:1}\) - remove one record
>
> **\(static method\)** removeById\(id: string \| number, options:QueryOptions ={limit:1}\) - remove by id
>
> **\(instance method\)** remove\(query: any = {}, options?: QueryOptions\) - remove the record itself

**Save \(create\)**

> **\(instance method\)** save\(options?: QueryOptions\) - Save instance to DB\Microservice

**Update**

> **\(static method\)** updateById\(id: string \| number, options:QueryOptions ={limit:1}\) - update by id
>
> **\(instance method\)** update\(options?: QueryOptions\) - Update instance on DB\Microservice




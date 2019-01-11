---
description: >-
  QueryOptions is an object which provides the query meta-data like sort, offset
  and limit
---

# QueryOptions \(sort, page, limit\)

QueryOptions class contains a `builder` method for easy "inline" usage.

**Properties**

> limit:number - The maximum records amount to query. default - 0.
>
> offset:number - The amount of record which should be skipped, can also be use for page number. default - 0.
>
> sort:Array - Array of sorted fields and their sort direction - SortItem

```text
SortItem{
    sortOption: SortOptions;// "DESC" | "ASC"
    field: string;
}
```

**Usage example**

```text
public static pagingQuery(query:any,limit:number,page:number){
    DataModel.findAll(query, QueryOptions.builder()
                        .setLimit(limit)
                        .setOffset(page)
                        .setSortOption(
                            new SortItem(SortOptions.DESC, "amount"),
                            new SortItem(SortOptions.ASC, "lastUpdate")
                        )
                    );
}
```


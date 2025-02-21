---
title: .alter-merge table update policy command - Azure Data Explorer
description: This article describes the .alter-merge table update policy command in Azure Data Explorer.
ms.reviewer: yonil
ms.topic: reference
ms.date: 09/27/2022
---
# .alter-merge table update policy

Change the table update policy. The [update policy](updatepolicy.md) instructs Azure Data Explorer to automatically append data to a target table whenever new data is inserted into the source table, based on a transformation query that runs on the data inserted into the source table.

> [!NOTE]
> The source table and the table for which the update policy is defined must be in the same database.
> The update policy function schema and the target table schema must match in their column names, types, and order.
> If the policy already defined on the table, the PolicyObjects specified in the command are added to the array of PolicyObjects in the existing policy.

## Syntax

`.alter-merge` `table` *TableName* `policy` `update` *ArrayOfPolicyObjects*
`.alter-merge` `table` *DatabaseName*`.`*TableName* `update` `sharding` *ArrayOfPolicyObjects*

## Arguments

*DatabaseName* - Specify the name of the database.
*TableName* - Specify the name of the table. Use without *DatabaseName* when running in the required database's context. A wildcard (*) denotes all tables.
*ArrayOfPolicyObjects* - Define policy objects, see also [update policy](updatepolicy.md).

## Returns

Returns a JSON representation of the policy.

## Example

Change the update policy for a table (using [multi-line string literals](../query/scalar-data-types/string.md#multi-line-string-literals)):

````kusto
.alter-merge table MyDatabase.MyTable policy update
```
[
    {
        "IsEnabled": true,
        "Source": "MyTableX",
        "Query": "MyOtherTable",
        "IsTransactional": true,
        "PropagateIngestionProperties": false
    }
]
```
````

---
title: series_add() - Azure Data Explorer
description: Learn how to use the series_add() function to calculate the element-wise addition of two numeric series inputs.
ms.reviewer: alexans
ms.topic: reference
ms.date: 01/22/2023
---
# series_add()

Calculates the element-wise addition of two numeric series inputs.

## Syntax

`series_add(`*series1*`,` *series2*`)`

## Arguments

* *series1, series2*: Input numeric arrays to be element-wise added into a dynamic array result. All arguments must be dynamic arrays. 

## Returns

Dynamic array of calculated element-wise add operation between the two inputs. Any non-numeric element or non-existing element (arrays of different sizes) yields a `null` element value.

## Example

<!-- csl: https://help.kusto.windows.net/Samples -->
```kusto
range x from 1 to 3 step 1
| extend y = x * 2
| extend z = y * 2
| project s1 = pack_array(x,y,z), s2 = pack_array(z, y, x)
| extend s1_add_s2 = series_add(s1, s2)
```

**Output**

|s1|s2|s1_add_s2|
|---|---|---|
|[1,2,4]|[4,2,1]|[5,4,5]|
|[2,4,8]|[8,4,2]|[10,8,10]|
|[3,6,12]|[12,6,3]|[15,12,15]|

---
title: series_multiply() - Azure Data Explorer
description: Learn how to use the series_multiply() function to calculate the element-wise multiplication of two numeric series inputs.
ms.reviewer: alexans
ms.topic: reference
ms.date: 01/25/2023
---
# series_multiply()

Calculates the element-wise multiplication of two numeric series inputs.

## Syntax

`series_multiply(`*series1*`,` *series2*`)`

## Arguments

* *series1, series2*: Input numeric arrays, to be element-wise multiplied into a dynamic array result. All arguments must be dynamic arrays.

## Returns

Dynamic array of calculated element-wise multiplication operation between the two inputs. Any non-numeric element or non-existing element (arrays of different sizes) yields a `null` element value.

## Example

<!-- csl: https://help.kusto.windows.net/Samples -->
```kusto
range x from 1 to 3 step 1
| extend y = x * 2
| extend z = y * 2
| project s1 = pack_array(x,y,z), s2 = pack_array(z, y, x)
| extend s1_multiply_s2 = series_multiply(s1, s2)
```

**Output**

|s1	        |s2|	    s1_multiply_s2|
|---|---|---|
|[1,2,4]	|[4,2,1]|	[4,4,4]|
|[2,4,8]	|[8,4,2]|	[16,16,16]|
|[3,6,12]	|[12,6,3]|	[36,36,36]|

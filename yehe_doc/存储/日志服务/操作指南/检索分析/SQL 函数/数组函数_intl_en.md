This document introduces the basic syntax and examples of array functions.

<table>
	<tr><th>Function</th><th>Syntax</th><th>Description</th></tr>
	<tr><td><a href="#subscript">Subscript operator: []</a></td><td>[x]</td><td>Returns an element from an array. Equivalent to the `element_at` function.</td></tr>
	<tr><td><a href="#array_agg">array_agg</a></td><td>array_agg(x)</td><td>Returns all values in `x` as an array.</td></tr>
	<tr><td><a href="#array_distinct">array_distinct</a></td><td>array_distinct(x)</td><td>Deduplicates an array and returns unique values from the array.</td></tr>
	<tr><td><a href="#array_except">array_except</a></td><td>array_except(x, y)</td><td>Returns the difference between the `x` and `y` arrays.</td></tr>
	<tr><td><a href="#array_intersect">array_intersect</a></td><td>array_intersect(x, y)</td><td>Returns the intersection between the `x` and `y` arrays.</td></tr>
	<tr><td rowspan=2><a href="#array_join">array_join</a></td><td>array_join(x, delimiter)</td><td>Concatenates the elements in an array using the specified delimiter. If the array contains a null element, the null element is ignored.</br><b>Note: </b>For the `array_join` function, the maximum return result supported is 1 KB, and data exceeding 1 KB will be truncated.</td></tr>
	<tr><td>array_join(x, delimiter, null_replacement)</td><td>Concatenates the elements in an array using `delimiter` and uses `null_replacement` to replace null values.</br><b>Note: </b>For the `array_join` function, the maximum return result supported is 1 KB, and data exceeding 1 KB will be truncated.</td></tr>
	<tr><td><a href="#array_max">array_max</a></td><td>array_max(x)</td><td>Returns the maximum value of an array.</td></tr>
	<tr><td><a href="#array_min">array_min</a></td><td>array_max(x)</td><td>Returns the minimum value of an array.</td></tr>
	<tr><td><a href="#array_position">array_position</a></td><td>array_position(x, element)</td><td>Returns the subscript (starting from 1) of a specified element. If the specified element does not exist, return `0`.</td></tr>
	<tr><td><a href="#array_remove">array_remove</a></td><td>array_remove(x, element)</td><td>Removes a specified element from an array.</td></tr>
	<tr><td><a href="#array_sort">array_sort</a></td><td>array_sort(x)</td><td>Sorts elements in an array in ascending order. If there are null elements, the null elements will be placed at the end of the returned array.</td></tr>
	<tr><td><a href="#array_union">array_union</a></td><td>array_union(x, y)</td><td>Returns the union of two arrays.</td></tr>
	<tr><td><a href="#cardinality">cardinality</a></td><td>cardinality(x)</td><td>Calculates the number of elements in an array.</td></tr>
	<tr><td><a href="#concat">concat</a></td><td>concat(x, y...)</td><td>Concatenates multiple arrays into one.</td></tr>
	<tr><td><a href="#contains">contains</a></td><td>contains(x, element)</td><td>Determines whether an array contains a specified element and returns `true` if the array contains the element.</td></tr>
	<tr><td><a href="#element_at">element_at</a></td><td>element_at(x, y)</td><td>Returns the yth element of an array.</td></tr>
	<tr><td><a href="#filter">filter</a></td><td>filter(x, lambda_expression)</td><td>Filters elements in an array and returns only the elements that comply with the Lambda expression.</td></tr>
	<tr><td><a href="#flatten">flatten</a></td><td>flatten(x)</td><td>Converts a two-dimensional array to a one-dimensional array.</td></tr>
	<tr><td><a href="#reduce">reduce</a></td><td>reduce(x, lambda_expression)</td><td>Adds the elements in the array as defined by the Lambda expression and returns the result.</td></tr>
	<tr><td><a href="#reverse">reverse</a></td><td>reverse(x)</td><td>Reverses the elements in an array.</td></tr>
	<tr><td rowspan=2><a href="#sequence">sequence</a></td><td>sequence(x, y)</td><td>Returns an array of consecutive and increasing values within the specified starting value range. The increment interval is the default value 1.</td></tr>
	<tr><td>sequence(x, y, step)</td><td>Returns an array of consecutive and increasing values within the specified starting value range. The increment interval is `step`.</td></tr>
	<tr><td><a href="#shuffle">shuffle</a></td><td>shuffle(x)</td><td>Randomizes the elements in an array.</td></tr>
	<tr><td><a href="#slice">slice</a></td><td>slice(x, start, length)</td><td>Returns a subset of an array.</td></tr>
	<tr><td><a href="#transform">transform</a></td><td>transform(x, lambda_expression)</td><td>Applies a Lambda expression to each element of an array.</td></tr>
	<tr><td><a href="#zip">zip</a></td><td>	zip(x, y)</td><td>Combines multiple arrays into a two-dimensional array (elements with the same subscript in each original array form a new array).</td></tr>
	<tr><td><a href="#zip_with">zip_with</a></td><td>zip_with(x, y, lambda_expression)</td><td>Merges two arrays into one as defined by a Lambda expression.</td></tr>
</table>

<span id="subscript"></span>
## Subscript Operator []

The subscript operator ([]) is used to return the xth element in an array. It is equivalent to the `element_at` function.

#### Syntax

```
[x]
```

#### Parameter description

| Parameter | Description |
| ---- | --------------------------------------- |
| x    | Array subscript, starting from 1. The parameter value is of the bigint type. |

#### Returned value type

Return the data type of the specified element.

#### Sample

Return the second element of the `number` field value.

- Field sample
```
array:[12,23,26,48,26]
```
- Search and analysis statement
```
* | SELECT cast(json_parse(array) as array(bigint)) [2]
```
- Search and analysis result

  
	

<span id="array_agg"></span>
## array_agg

The `array_agg` function is used to return all values in `x` as an array.

#### Syntax

```
array_agg(x)
```

#### Parameter description

| Parameter | Description |
| ---- | ---------------------- |
| x    | The parameter value can be of any data type.           |

#### Returned value type

Array

#### Sample

Return the values of the `status` field as an array.

- Search and analysis statement
```
* | SELECT array_agg(status) AS array
```
- Search and analysis result


<span id="array_distinct"></span>
## array_distinct

The `array_distinct` function is used to delete duplicate elements from an array.

#### Syntax

```
array_distinct(x)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |

#### Returned value type

Array

#### Sample

Delete duplicate elements from the `array` field.

- Field sample
```
array:[12,23,26,48,26]
```
- Search and analysis statement
```
* | SELECT array_distinct(cast(json_parse(array) as array(bigint)))
```
- Search and analysis result



<span id="array_except"></span>
## array_except

The `array_except` function is used to calculate the difference between two arrays.

#### Syntax

```
array_except(x, y)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |
| y    | The parameter value is of the array type. |

#### Returned value type

Array

#### Sample

Calculate the difference between arrays [1,2,3,4,5] and [1,3,5,7].

- Search and analysis statement
```
* | SELECT array_except(array[1,2,3,4,5],array[1,3,5,7])
```
- Search and analysis result



<span id="array_intersect"></span>
## array_intersect

The `array_intersect` function is used to calculate the intersection between two arrays.

#### Syntax

```
array_intersect(x, y)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |
| y    | The parameter value is of the array type. |

#### Returned value type

Array

#### Sample

Calculate the difference between arrays [1,2,3,4,5] and [1,3,5,7].

- Search and analysis statement
```
* | SELECT array_intersect(array[1,2,3,4,5],array[1,3,5,7])
```
- Search and analysis result


<span id="array_join"></span>
## array_join

The `array_join` function is used to concatenate the elements in an array into a string using the specified delimiter.

#### Syntax

- Concatenate the elements in an array into a string using the specified delimiter. If the array contains null elements, the null elements are ignored.
```
array_join(x, delimiter)
```
- Concatenate the elements in an array into a string using the specified delimiter. If the array contains null elements, the null elements are replaced with `null_replacement`.
```
array_join(x, delimiter, null_replacement)
```

#### Parameter description

| Parameter | Description |
| ---------------- | -------------------------- |
| x                | The parameter value is of the array type.        |
| delimiter        | Connector, which can be a string.     |
| null_replacement | String used to replace a null element. |

#### Returned value type

Varchar

#### Sample

Use spaces to concatenate the elements in the [null,'China','sh'] array as a string, and replace the null element with `region`.

- Search and analysis statement
```
* | SELECT array_join(array[null,'China','sh'],'/','region')
```
- Search and analysis result



<span id="array_max"></span>
## array_max

The `array_max` function is used to get the maximum value of an array.

#### Syntax

```
array_max(x)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |

#### Returned value type

Same as the element data type of the parameter value.

#### Sample

Get the maximum value 48 from the [12,23,26,48,26] array.

- Field sample
```
array:[12,23,26,48,26]
```
- Search and analysis statement
```
* | SELECT array_max(try_cast(json_parse(array) as array(bigint))) AS max_number
```
- Search and analysis result



<span id="array_min"></span>
## array_min

The `array_min` function is used to get the minimum value of an array.

#### Syntax

```
array_min(x)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |

#### Returned value type

Same as the element data type of the parameter value.

#### Sample

Get the minimum value 12 from the [12,23,26,48,26] array.

- Field sample
```
array:[12,23,26,48,26]
```
- Search and analysis statement
```
* | SELECT array_min(try_cast(json_parse(array) as array(bigint))) AS min_number
```
- Search and analysis result


<span id="array_position"></span>
## array_position

The `array_position` function is used to get the subscript (starting from 1) of a specified element. If the specified element does not exist, return `0`.

#### Syntax

```
array_position(x, element)
```

#### Parameter description

| Parameter | Description |
| ------- | ------------------ |
| x       | The parameter value is of the array type. |
| element | Element in an array. |

#### Returned value type

Bigint

#### Sample

Return the subscript of 46 in the [23,46,35] array.

- Search and analysis statement
```
* | SELECT array_position(array[23,46,35],46)
```
- Search and analysis result


<span id="array_remove"></span>
## array_remove

The `array_remove` function is used to delete a specified element from an array.

#### Syntax

```
array_remove(x, element)
```

#### Parameter description

| Parameter | Description |
| ------- | ------------------ |
| x       | The parameter value is of the array type. |
| element | Element in an array. |

#### Returned value type

Array

#### Sample

Delete 23 from the [23,46,35] array.

- Search and analysis statement
```
* | SELECT array_remove(array[23,46,35],23)
```
- Search and analysis result


<span id="array_sort"></span>
## array_sort

The `array_sort` function is used to sort elements in an array in ascending order.

#### Syntax

```
array_sort(x)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |

#### Returned value type

Array

#### Sample

Sort elements in the ['b', 'd', null, 'c', 'a'] array in ascending order.

- Search and analysis statement
```
* | SELECT array_sort(array['b','d',null,'c','a'])
```
- Search and analysis result


<span id="array_union"></span>
## array_union

The `array_union` function is used to calculate the union of two arrays.

#### Syntax

```
array_union(x, y)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |
| y    | The parameter value is of the array type. |

#### Returned value type

Array

#### Sample

Calculate the union of the arrays [1,2,3,4,5] and [1,3,5,7].

- Search and analysis statement
```
* | SELECT array_union(array[1,2,3,4,5],array[1,3,5,7])
```
- Search and analysis result



<span id="cardinality"></span>
## cardinality

The `cardinality` function is used to calculate the number of elements in an array.

#### Syntax

```
cardinality(x)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |

#### Returned value type

Bigint

#### Sample

Calculate the number of elements in the `number` field value.

- Field sample
```
array:[12,23,26,48,26]
```
- Search and analysis statement
```
* | SELECT cardinality(cast(json_parse(array) as array(bigint)))
```
- Search and analysis result



<span id="concat"></span>
## concat

The `concat` function is used to concatenate multiple arrays into one.

#### Syntax

```
concat(x, y...)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |
| y    | The parameter value is of the array type. |

#### Returned value type

Array

#### Sample

Concatenate the arrays ['red','blue'] and ['yellow','green'] into one array.

- Search and analysis statement
```
* | SELECT concat(array['red','blue'],array['yellow','green'])
```
- Search and analysis result



<span id="contains"></span>
## contains

The `contains` function is used to determine whether an array contains a specified element and return `true` if the array contains the element.

#### Syntax

```
contains(x, element)
```

#### Parameter description

| Parameter | Description |
| ------- | ------------------ |
| x       | The parameter value is of the array type. |
| element | Element in an array. |

#### Returned value type

Boolean

#### Sample

Determine whether the `array` field value contains 23.

- Field sample
```
array:[12,23,26,48,26]
```
- Search and analysis statement
```
* | SELECT contains(cast(json_parse(array) as array(varchar)),'23')
```
- Search and analysis result


<span id="element_at"></span>
## element_at

The `element_at` function is used to return the yth element in an array.

#### Syntax

```
element_at(x, y)
```

#### Parameter description

| Parameter | Description |
| ------- | --------------------------------------- |
| x                | The parameter value is of the array type.        |
| element    | Array subscript, starting from 1. The parameter value is of the bigint type. |

#### Returned value type

Any data type

#### Sample

Return the second element of the `number` field value.

- Field sample
```
array:[12,23,26,48,26]
```
- Search and analysis statement
```
* | SELECT element_at(cast(json_parse(number) AS array(varchar)), 2)
```
- Search and analysis result



<span id="filter"></span>
## filter

The `filter` function is used to filter elements in an array and return only the elements that comply with a specified Lambda expression

#### Syntax

```
filter(x, lambda_expression)
```

#### Parameter description

| Parameter | Description |
| ----------------- | ------------------------------------------------------------ |
| x                 | The parameter value is of the array type.                                          |
| lambda_expression | Lambda expression. For more information, see [Lambda Function](https://intl.cloud.tencent.com/document/product/614/43564). |

#### Returned value type

Array

#### Sample

Return elements greater than 0 in the [5,-6,null,7] array, where `x -> x > 0` is the Lambda expression.

- Search and analysis statement
```
* | SELECT filter(array[5,-6,null,7],x -> x > 0)
```
- Search and analysis result



<span id="flatten"></span>
## flatten

The `flatten` function is used to convert a two-dimensional array to a one-dimensional array.

#### Syntax

```
flatten(x)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |

#### Returned value type

Array

#### Sample

Convert the two-dimensional array "array[1,2,3,4],array[4,3,2,1]" into a one-dimensional array.

- Search and analysis statement
```
* | SELECT flatten(array[array[1,2,3,4],array[4,3,2,1]])
```
- Search and analysis result



<span id="reduce"></span>
## reduce

The `reduce` function is used to add the elements in an array as defined by the Lambda expression and return the result.

#### Syntax

```
reduce(x, lambda_expression)
```

#### Parameter description

| Parameter | Description |
| ----------------- | ------------------------------------------------------------ |
| x                 | The parameter value is of the array type.                                          |
| lambda_expression | Lambda expression. For more information, see [Lambda Function](https://intl.cloud.tencent.com/document/product/614/43564). |

#### Returned value type

Bigint

#### Sample

Return the sum of the elements in array [5, 20, 50].

- Search and analysis statement
```
* | SELECT reduce(array[5,20,50],0,(s, x) -> s + x, s -> s)
```
- Search and analysis result



<span id="reverse"></span>
## reverse

The `reverse` function is used to reverse the elements in an array.

#### Syntax

```
reverse(x)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |

#### Returned value type

Array

#### Sample

Reverse the elements in array [1,2,3,4,5].

- Search and analysis statement
```
* | SELECT reverse(array[1,2,3,4,5])
```
- Search and analysis result



<span id="sequence"></span>
## sequence

The `sequence` function is used to return an array of consecutive and increasing values within the specified starting value range.

#### Syntax

- The increment interval is the default value `1`.
```
sequence(x, y)
```
- The increment interval is custom.
```
sequence(x, y, step)
```

#### Parameter description

| Parameter                    | Description                                                         |
| ---- | ------------------------------------------------------------ |
| x    | The parameter value is of the bigint or timestamp type (UNIX timestamp or date and time expression). |
| y    | The parameter value is of the bigint or timestamp type (UNIX timestamp or date and time expression). |
| step | Value interval.</br>If the parameter value is a date and time expression, the format of `step` is as follows:<br/>- interval  'n' year to month: the interval is `n` years.<br/>- interval  'n' day to second: the interval is `n` days. |

#### Returned value type

Array

#### Sample

Example 1. Return even numbers between 0 and 10.

- Search and analysis statement
```
* | SELECT sequence(0,10,2)
```
- Search and analysis result


Example 2. Return dates between 2017-10-23 and 2021-08-12 at an interval of one year.

- Search and analysis statement
```
* | SELECT sequence(from_unixtime(1508737026),from_unixtime(1628734085),interval '1' year to month )
```
- Search and analysis result


Example 3. Return UNIX timestamps between 1628733298 and 1628734085 at an interval of 60 seconds.

- Search and analysis statement
```
* | SELECT sequence(1628733298,1628734085,60)
```
- Search and analysis result



<span id="shuffle"></span>
## shuffle

The `shuffle` function is used to randomize the elements in an array.

#### Syntax

```
shuffle(x)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------- |
| x    | The parameter value is of the array type. |

#### Returned value type

Array

#### Sample

Randomize the elements in the [1,2,3,4,5] array.

- Search and analysis statement
```
* | SELECT shuffle(array[1,2,3,4,5])
```
- Search and analysis result


<span id="slice"></span>
## slice

The `slice` function is used to return a subset of an array.

#### Syntax

```
slice(x, start, length)
```

#### Parameter description

| Parameter | Description |
| ------ | ------------------------------------------------------------ |
| x                 | The parameter value is of the array type.                                          |
| start  | Index start position.<br>- If `start` is negative, start from the end.<br/>- If `start` is positive, start from the beginning. |
| length | Number of elements in a subset.                                       |

#### Returned value type

Array

#### Sample

Return a subset of the [1,2,4,5,6,7,7] array, starting from the third element and consisting of two elements.

- Search and analysis statement
```
* | SELECT slice(array[1,2,4,5,6,7,7],3,2)
```
- Search and analysis result


<span id="transform"></span>
## transform

The `transform` function is used to apply a Lambda expression to each element of an array.

#### Syntax

```
transform(x, lambda_expression)
```

#### Parameter description

| Parameter | Description |
| ----------------- | ------------------------------------------------------------ |
| x                 | The parameter value is of the array type.                                          |
| lambda_expression | Lambda expression. For more information, see [Lambda Function](https://intl.cloud.tencent.com/document/product/614/43564). |

#### Returned value type

Array

#### Sample

Increment each element in the [5,6] array by 1 and return.

- Search and analysis statement
```
* | SELECT transform(array[5,6],x -> x + 1)
```
- Search and analysis result



<span id="zip"></span>
## zip

The `zip` function is used to combine multiple arrays into a two-dimensional array, and elements with the same subscript in each original array form a new array.

#### Syntax

```
zip(x, y)
```

#### Parameter description

| Parameter | Description |
| :--- | :-------------------- |
| x    | The parameter value is of the array type. |
| y    | The parameter value is of the array type. |

#### Returned value type

Array

#### Sample

Combine the arrays [1,2] and [3,4] into a two-dimensional array.

- Search and analysis statement
```
* | SELECT zip(array[1,2], array[3,4])
```
- Search and analysis result
```
["{1, 3}","{2, 4}"]
```

 

<span id="zip_with"></span>
## zip_with

The `zip_with` function is used to merge two arrays into one as defined by a Lambda expression.

#### Syntax

```
zip_with(x, y, lambda_expression)
```

#### Parameter description

| Parameter | Description |
| ----------------- | ------------------------------------------------------------ |
| x                 | The parameter value is of the array type.                                          |
| y                 | The parameter value is of the array type.                                          |
| lambda_expression | Lambda expression. For more information, see [Lambda Function](https://intl.cloud.tencent.com/document/product/614/43564). |

#### Returned value type

Array

#### Sample

Use Lambda expression `(x, y) -> x + y` to add the elements in arrays [1,2] and [3,4], respectively, and return the sum results as an array.

- Search and analysis statement
```
* | SELECT zip_with(array[1,2], array[3,4],(x,y) -> x + y)
```
- Search and analysis result




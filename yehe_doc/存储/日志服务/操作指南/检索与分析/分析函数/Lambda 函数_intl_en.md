This document introduces the basic syntax and examples of Lambda functions.

CLS allows you to define Lambda expressions in SQL analysis statements and pass them to specified functions to enrich the expressions of functions.

### Syntax

Lambda expressions need to be used together with functions such as [filter](https://intl.cloud.tencent.com/document/product/614/43565#filter), [reduce](https://intl.cloud.tencent.com/document/product/614/43565#reduce), [transform](https://intl.cloud.tencent.com/document/product/614/43565#transform), and [zip_with](https://intl.cloud.tencent.com/document/product/614/43565#zip_with). The syntax of a Lambda expression is as follows:
```
parameter -> expression
```

<table>
	<tr><th>Parameter</th><th>Description</th></tr>
	<tr><td>parameter</td><td>Identifier used to pass the parameter.</td></tr>
	<tr><td>expression</td><td>Expression. Most MySQL expressions can be used in Lambda expressions, such as:</br>
	<pre><code>x -> x + 1 <br/>(x, y) -> x + y <br/>x -> regexp_like(x, 'a+') <br/>x -> x[1] / x[2] <br/>x -> if(x > 0, x, -x) <br/>x -> coalesce(x, 0) <br/>x -> cast(x AS JSON) <br/>x -> x + try(1 / 0)</code></pre></td></tr>
</table>


### Example

#### Example 1. Using the Lambda expression "x-> x is not null"

Return non-null elements in the [5, null, 7, null] array.

- Query and analysis statement
```
* | SELECT filter(array[5, null, 7, null], x -> x is not null)
```
- Query and analysis result


#### Example 2. Using the Lambda expression "0, (s, x) -> s + x, s -> s"

Return the sum of the elements in array [5, 20, 50].

- Query and analysis statement
```
* | SELECT reduce(array[5, 20, 50], 0, (s, x) -> s + x, s -> s)
```
- Query and analysis result



#### Example 3. Using the Lambda expression "(k, v) -> v> 10"

Map two arrays to a map with a key value greater than 10.

- Query and analysis statement
```
* | SELECT map_filter(map(array['class01', 'class02', 'class03'], array[11, 10, 9]), (k,v) -> v > 10)
```
- Query and analysis result


#### Example 4. Using the Lambda expression "(x, y) -> (y, x)"

Swap the positions of two elements in an array and extract the elements with the same index to form a new two-dimensional array.

- Query and analysis statement
```
* | SELECT zip_with(array['a', 'b', 'c'], array['d', 'e', 'f'], (x, y) -> concat(x, y))
```
- Query and analysis result


#### Example 5. Using the Lambda expression "x -> coalesce (x, 0) +1"

Increment each element in the [5, NULL, 6] array by 1 and return. If the array contains a null element, the null element is converted to 0 and then incremented by 1.

- Query and analysis statement
```
* | SELECT transform(array[5, NULL, 6], x -> coalesce(x, 0) + 1)
```
- Query and analysis result


#### Other examples

```
* | SELECT filter(array[], x -> true)
* | SELECT map_filter(map(array[],array[]), (k, v) -> true)
* | SELECT reduce(array[5, 6, 10, 20], -- calculates arithmetic average: 10.25
              cast(row(0.0, 0) AS row(sum double, count integer)),
              (s, x) -> cast(row(x + s.sum, s.count + 1) AS row(sum double, count integer)),
              s -> if(s.count = 0, null, s.sum / s.count))
* | SELECT reduce(array[2147483647, 1], cast(0 AS bigint), (s, x) -> s + x, s -> s)
* | SELECT reduce(array[5, 20, null, 50], 0, (s, x) -> s + x, s -> s)
* | SELECT transform(array[array[1, null, 2], array[3, null]], a -> filter(a, x -> x is not null))
```


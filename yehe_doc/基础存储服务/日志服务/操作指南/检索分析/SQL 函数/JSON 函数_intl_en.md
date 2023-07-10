This document introduces the basic syntax and examples of JSON functions.

<table>
	<tr><th>Function</th><th>Syntax</th><th>Description</th></tr>
	<tr><td><a href="#json_array_contains">json_array_contains</a></td><td>json_array_contains(x, value)</td><td>Determines whether a JSON array contains a given value.</td></tr>
	<tr><td><a href="#json_array_get">json_array_get</a></td><td>json_array_get(x, index)</td><td>Returns the element with the specified index in a given JSON array.</td></tr>
	<tr><td><a href="#json_array_length">json_array_length</a></td><td>json_array_length(x) </td><td>Returns the number of elements in a given JSON array. If `x` is not a JSON array, `null` will be returned.</td></tr>
	<tr><td><a href="#json_extract">json_extract</a></td><td>json_extract(x, json_path)</td><td>Extracts a set of JSON values (array or object) from a JSON object or array.</td></tr>
	<tr><td><a href="#json_extract_scalar">json_extract_scalar</a></td><td>json_extract_scalar(x, json_path)</td><td>Extracts a set of scalar values (strings, integers, or Boolean values) from a JSON object or array. Similar to the `json_extract` function.</td></tr>
	<tr><td><a href="#json_format">json_format</a></td><td>json_format(x)</td><td>Converts a JSON value into a string value.</td></tr>
	<tr><td><a href="#json_parse">json_parse</a></td><td>json_parse(x)</td><td>Converts a string value into a JSON value.</td></tr>
	<tr><td><a href="#json_size">json_size</a></td><td>json_size(x, json_path)</td><td>Calculates the number of elements in a JSON object or array.</td></tr>
</table>

<span id="json_array_contains"></span>
## json_array_contains

The `json_array_contains` function is used to determine whether a JSON array contains a specified value.

### Syntax

```
json_array_contains(x, value)
```

### Parameter description

| Parameter | Description |
| ----- | ------------------ |
| x     | The parameter value is a JSON array. |
| value | Value.             |

### Return value type

Boolean

### Example

Determine whether the JSON array [1, 2, 3] contains 2.

- Search and analysis statement
```
* | SELECT json_array_contains('[1, 2, 3]', 2)
```
- Search and analysis result



<span id="json_array_get"></span>
## json_array_get

The `json_array_get` function is used to get the element with a specified index in a JSON array.

### Syntax

```
json_array_get(x, index)
```

### Parameter description

| Parameter | Description |
| ----- | ------------------- |
| x     | The parameter value is a JSON array. |
| index | JSON subscript (index), starting from 0. |

### Return value type

Varchar

### Example

Return the element with index 1 in the JSON array ["a", [3, 9], "c"].

- Search and analysis statement
```
* | SELECT json_array_get('["a", [3, 9], "c"]', 1)
```
- Search and analysis result



<span id="json_array_length"></span>
## json_array_length

The `json_array_length` function is used to calculate the number of elements in a JSON array. If `x` is not a JSON array, `null` will be returned.

### Syntax

```
json_array_length(x)
```

### Parameter description

| Parameter | Description |
| ---- | ------------------ |
| x     | The parameter value is a JSON array. |

### Return value type

Bigint

### Example

- Example 1. Calculate the number of JSON elements in the **apple.message** field
  - Field sample
```
apple.message:[{"traceName":"StoreMonitor"},{"topicName":"persistent://apache/pulsar/test-partition-17"},{"producerName":"pulsar-mini-338-36"},{"localAddr":"pulsar://pulsar-mini-broker-5.pulsar-mini-broker.pulsar.svc.cluster.local:6650"},{"sequenceId":826},{"storeTime":1635905306062},{"messageId":"19422-24519"},{"status":"SUCCESS"}]
```
- Search and analysis statement
```
* | SELECT json_array_length(apple.message)
```
- Search and analysis result


<span id="json_extract"></span>
## json_extract

The `json_extract` function is used to extract a set of JSON values (array or object) from a JSON object or array.

### Syntax

```
json_extract(x, json_path)
```

### Parameter description

| Parameter | Description |
| --------- | --------------------------------------- |
| x         | The parameter value is a JSON object or array.            |
| json_path | [JSONPath](https://goessner.net/articles/JsonPath/), such as `$.store.book[0].title`.</br>Note: JSON syntax requiring array element traversal is not supported, such as the following: `$.store.book[*].author`, `$..book[(@.length-1)]`, `$..book[?(@.price<10)]`. |

### Return value type

JSON string

### Example

Get the value of **epochSecond** in the **apple.instant** field.

- Field sample
```
apple.instant:{"epochSecond":1635905306,"nanoOfSecond":63001000}
```
- Search and analysis statement
```
* | SELECT json_extract(apple.instant, '$.epochSecond')
```
- Search and analysis result



<span id="json_extract_scalar"></span>
## json_extract_scalar

The `json_extract_scalar` function is used to extract a set of scalar values (strings, integers, or Boolean values) from a JSON object or array.

### Syntax

```
json_extract_scalar(x, json_path)
```

### Parameter description

| Parameter | Description |
| --------- | --------------------------------------- |
| x         | The parameter value is a JSON array.                      |
| json_path | [JSONPath](https://goessner.net/articles/JsonPath/), such as `$.store.book[0].title`.</br>Note: JSON syntax requiring array element traversal is not supported, such as the following: `$.store.book[*].author`, `$..book[(@.length-1)]`, `$..book[?(@.price<10)]`. |

### Return value type

Varchar

### Example

Get the value of **epochSecond** from the **apple.instant** field and convert the value into a bigint value for summation.

- Field sample
```
apple.instant:{"epochSecond":1635905306,"nanoOfSecond":63001000}
```
- Search and analysis statement
```
* | SELECT sum(cast(json_extract_scalar(apple.instant,'$.epochSecond') AS bigint) )
```
- Search and analysis result



<span id="json_format"></span>
## json_format

The `json_format` function is used to convert a JSON value into a string value.

### Syntax

```
json_format(x)
```

### Parameter description

| Parameter | Description |
| ---- | ------------------ |
| x    | The parameter value is of JSON type. |

### Return value type

Varchar

### Example

Convert the JSON array [1,2,3] into a string [1, 2, 3].

- Search and analysis statement
```
* | SELECT json_format(json_parse('[1, 2, 3]'))
```
- Search and analysis result



<span id="json_parse"></span>
## json_parse

The `json_parse` function is used to convert a string value into a JSON value and determine whether it complies with the JSON format.

### Syntax

```
json_parse(x)
```

### Parameter description

| Parameter | Description |
| ---- | ---------------- |
| x    | The parameter value is a string. |

### Return value type

JSON

### Example

Convert the JSON array [1,2,3] into a string [1, 2, 3].

- Search and analysis statement
```
* | SELECT json_parse('[1, 2, 3]')
```
- Search and analysis result


<span id="json_size"></span>
## json_size

The `json_size` function is used to calculate the number of elements in a JSON object or array.

### Syntax

```
json_size(x, json_path)
```

### Parameter description

| Parameter | Description |
| --------- | ---------------------------- |
| x         | The parameter value is a JSON object or array.            |
| json_path | JSON path, in the format of `$.store.book[0].title`. |

### Return value type

Bigint

### Example

Convert the JSON array [1,2,3] into a string [1, 2, 3].

- Search and analysis statement
```
* | SELECT json_size(json_parse('[1, 2, 3]'),'$')
```
- Search and analysis result




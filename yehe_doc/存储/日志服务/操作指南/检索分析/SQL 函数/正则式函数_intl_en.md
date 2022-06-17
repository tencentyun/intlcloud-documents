This document introduces the basic syntax and examples of regular expression functions.

CLS supports the following regular expression functions:

<table>
	<tr><th>Function</th><th>Syntax</th><th>Description</th></tr>
	<tr><td rowspan=2><a href="#regexp_extract_all">regexp_extract_all</a></td><td>regexp_extract_all(x, regular expression) </td><td>Extracts the substrings that match a specified regular expression from a specified string and returns a collection of all matched substrings.</td></tr>
	<tr><td>regexp_extract_all(x, regular expression, n)</td><td>Extracts the substrings that match a specified regular expression from a specified string and returns a collection of substrings that match the target capture group.</td></tr>
	<tr><td rowspan=2><a href="#regexp_extract">regexp_extract</a></td><td>regexp_extract(x, regular expression) </td><td>Extracts and returns the first substring that matches a specified regular expression from a specified string.</td></tr>
	<tr><td>regexp_extract(x, regular expression, n)</td><td>Extracts the substrings that match a specified regular expression from a specified string and returns the first substring that matches the target capture group.</td></tr>
	<tr><td><a href="#regexp_like">regexp_like</a></td><td>regexp_like(x, regular expression)</td><td>Checks whether a specified string matches a specified regular expression.</td></tr>
	<tr><td rowspan=2><a href="#regexp_replace">regexp_replace</a></td><td>regexp_replace(x, regular expression)</td><td>Deletes the substrings that match a specified regular expression from a specified string and returns the substrings that are not deleted.</td></tr>
	<tr><td>regexp_replace(x, regular expression, replace string)</td><td>Replaces the substrings that match a specified regular expression in a specified string and returns the new string after the replacement.</td></tr>
	<tr><td><a href="#regexp_split">regexp_split</a></td><td>regexp_split(x, regular expression)</td><td>Splits a specified string into multiple substrings by using a specified regular expression and returns a collection of the substrings.</td></tr>
</table>


<span id="regexp_extract_all"></span>
## regexp_extract_all

The `regexp_extract_all` function is used to extract the substrings that match a specified regular expression from a specified string.

### Syntax

- Extract the substrings that match a specified regular expression from a specified string and return a collection of all matched substrings.
```
regexp_extract_all(x, regular expression)
```
- Extract the substrings that match a specified regular expression from a specified string and return a collection of substrings that match the target capture group.
```
regexp_extract_all(x, regular expression, n)
```

### Parameter description

| Parameter | Description |
| ------------------ | ----------------------------------------------------------- |
| x                  | The parameter value is of the varchar type.                                       |
| regular expression | The regular expression that contains capture groups. For example, `(\d)(\d)(\d)` indicates three capture groups. |
| n                  | The nth capture group. `n` is an integer that starts from 1.                             |

### Return value type

Array

### Example

Extract all numbers from the value of the `http_protocol` field.

- Query and analysis statement
```
* | SELECT regexp_extract_all(http_protocol, '\d+') 
```
- Query and analysis result


<span id="regexp_extract"></span>
## regexp_extract

The `regexp_extract` function is used to extract the first substring that matches a specified regular expression from a specified string.

### Syntax

- Extract and return the first substring that matches a specified regular expression from a specified string.
```
regexp_extract(x, regular expression)
```
- Extract the substrings that match a specified regular expression from a specified string and return the first substring that matches the target capture group.
```
regexp_extract(x, regular expression, n)
```

### Parameter description

| Parameter | Description |
| ------------------ | ----------------------------------------------------------- |
| x                  | The parameter value is of the varchar type.                                       |
| regular expression | The regular expression that contains capture groups. For example, `(\d)(\d)(\d)` indicates three capture groups. |
| n                  | The nth capture group. `n` is an integer that starts from 1.                             |

### Return value type

Varchar

### Example

#### Example 1. Extract the first number from the value of the `http_protocol` field

- Query and analysis statement
```
* | SELECT regexp_extract_all(http_protocol, '\d+') 
```
- Query and analysis result


#### Example 2. Extract the file information from the value of the `request_uri` field and count the number of times each file is accessed

- Query and analysis statement
```
* | SELECT regexp_extract(request_uri, '.*\/(index.*)', 1) AS file, count(*) AS count GROUP BY file
```
- Query and analysis result


<span id="regexp_like"></span>
## regexp_like

The `regexp_like` function is used to check whether a specified string matches a specified regular expression.

### Syntax

```
regexp_like (x, regular expression)
```

### Parameter description

| Parameter | Description |
| ------------------ | --------------------- |
| x                  | The parameter value is of the varchar type.                                       |
| regular expression | Regular expression.          |

### Return value type

Boolean

### Example

Check whether the value of the `server_protocol` field contains digits.

- Query and analysis statement
```
* | select regexp_like(server_protocol, '\d+')
```
- Query and analysis result


<span id="regexp_replace"></span>
## regexp_replace

The `regexp_replace` function is used to delete or replace the substrings that match a specified regular expression in a specified string.

### Syntax

- Delete the substrings that match a specified regular expression from a specified string and return the substrings that are not deleted.
```
regexp_replace (x, regular expression)
```
- Replace the substrings that match a specified regular expression in a specified string and return the new string after the replacement.
```
regexp_replace (x, regular expression, replace string)
```

### Parameter description

| Parameter | Description |
| ------------------ | --------------------- |
| x                  | The parameter value is of the varchar type.                                       |
| regular expression | Regular expression.          |
| replace string     | Substring that is used to replace the matched substring.       |

### Return value type

String

### Example

Delete the version number in the value of the `server_protocol` field and calculate the number of requests for each communication protocol.

- Query and analysis statement
```
* | select regexp_replace(server_protocol, '.\d+') AS server_protocol, count(*) AS count GROUP BY server_protocol
```
- Query and analysis result



<span id="regexp_split"></span>
## regexp_split

The `regexp_split` function is used to split a specified string into multiple substrings and return a collection of the substrings.

### Syntax

```
regexp_split (x, regular expression)
```

### Parameter description

| Parameter | Description |
| ------------------ | --------------------- |
| x                  | The parameter value is of the varchar type.                                       |
| regular expression | Regular expression.          |

### Return value type

Array

### Example

Split the value of the `server_protocol` field with forward slashes (/).

- Query and analysis statement
```
* | select regexp_split(server_protocol, '/')
```
- Query and analysis result






This document introduces the basic syntax and examples of type conversion functions.


If you need to distinguish more detailed data types when querying and analyzing data, you can use type conversion functions for data type conversion in query and analysis statements.

| Function     | Syntax                | Description                                                         |
| ------------ | ------------------- | ------------------------------------------------------------ |
| cast     | cast(x as type)     | Parses the data type of `x`.</br>During `cast` execution, if a value fails to be parsed, the system terminates the entire query and analysis operation. |
| try_cast | try_cast(x as type) | Parses the data type of `x`.</br>During `try_cast` execution, if a value fails to be parsed, the system returns `NULL` and continues processing by skipping the value. |
| typeof   |         typeof(x)  |         Returns the data type of `x`.   |

>? When dirty data may exist in logs, you are advised to use the `try_cast` function to avoid query and analysis failures caused by dirty data.
>

## Function cast

The `cast` function is used to parse the data type of `x`. During `cast` execution, if a value fails to be parsed, the system terminates the entire query and analysis operation.

### Syntax

```
cast(x as type)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------------------------------------------------ |
| x    | The parameter value can be of any type.                                       |
| type | SQL data type. Valid values: `bigint`, `varchar`, `double`, `boolean`, `timestamp`, `decimal`, `array`, or `map`.</br>For the mappings between index and SQL data types, please see [Appendix: Data Type Mappings](#DataTypeMapping). |

If `type` is `timestamp`, `x` must be a timestamp in milliseconds (such as 1597807109000) or a time string in the ISO 8601 time format (such as 2019-12-25T16:17:01+08:00).

#### Return value type

The return value type is determined by the `type` parameter.

#### Example

1. Parse the numeric value 0.01 into a BIGINT value:
```
* | select cast(0.01 as bigint)
```

2. Convert the CLS log collection time `__TIMESTAMP__` to `TIMESTAMP`.
```
* | select cast(__TIMESTAMP__ as timestamp)
```

## Function try_cast

The `try_cast` function is used to parse the data type of `x`. During `try_cast` execution, if a value fails to be parsed, the system returns `NULL` and continues processing by skipping the value.

#### Syntax

```
try_cast(x as type)
```

#### Parameter description

| Parameter | Description |
| ---- | ------------------------------------------------------------ |
| x    | The parameter value can be of any type.                                       |
| type | SQL data type. Valid values: `bigint`, `varchar`, `double`, `boolean`, `timestamp`, `decimal`, `array`, or `map`.</br>For the mappings between index and SQL data types, please see [Appendix: Data Type Mappings](#DataTypeMapping). |

#### Return value type

The return value type is determined by the `type` parameter.

#### Example

Parse the **remote_user** field value into a VARCHAR value:

```
* | select try_cast(remote_user as varchar)
```



<span id="DataTypeMapping"></span>

## Appendix: Data Type Mappings 

The mappings between index and SQL data types are as follows:

| Index Data Type | SQL Data Type |
| -------------- | -------------- |
| long           | bigint        |
| text           | varchar       |
| double         | double        |
| json           | varchar       |

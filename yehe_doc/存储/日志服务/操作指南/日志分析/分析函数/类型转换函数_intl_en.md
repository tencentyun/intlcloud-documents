This document introduces the basic syntax and examples of type conversion functions.

>? Currently, CLS functions can be used in most regions. If they are required in Beijing, Shanghai, Guangzhou, and Nanjing, please contact [smart customer service](https://intl.cloud.tencent.com/contact-sales).
>

If you need to distinguish more detailed data types when querying and analyzing data, you can use type conversion functions for data type conversion in query and analysis statements.

| Function     | Syntax                | Description                                                         |
| ------------ | ------------------- | ------------------------------------------------------------ |
| cast     | cast(x as type)     | Parses the data type of `x`.</br>During `cast` execution, if a value fails to be parsed, the system terminates the entire query and analysis operation. |
| try_cast | try_cast(x as type) | Parses the data type of `x`.</br>During `try_cast` execution, if a value fails to be parsed, the system returns `NULL` and continues processing by skipping the value. |

>? Dirty data may exist in logs. You are advised to use the `try_cast` function to avoid query and analysis failures caused by dirty data.
>

## Function cast

The `cast` function is used to parse the data type of `x`. During `cast` execution, if a value fails to be parsed, the system terminates the entire query and analysis operation.

### Syntax

```
cast(x as type)
```

### Parameters

| Parameter           | Description                                                         |
| ---- | ------------------------------------------------------------ |
| x    | The parameter value can be of any type.                                       |
| type | SQL data type. Valid values: `bigint`, `varchar`, `double`, `boolean`, `timestamp`, `decimal`, `array`, or `map`.</br>For the mappings between index and SQL data types, please see [Appendix: Data Type Mappings](#DataTypeMapping). |

### Return value type

The return value type is determined by the `type` parameter.

### Example

Parse the numeric value 0.01 into a BIGINT value:

```
* | select cast(0.01 as bigint)
```



## Function try_cast

The `try_cast` function is used to parse the data type of `x`. During `try_cast` execution, if a value fails to be parsed, the system returns `NULL` and continues processing by skipping the value.

### Syntax

```
try_cast(x as type)
```

### Parameters

| Parameter           | Description                                                         |
| ---- | ------------------------------------------------------------ |
| x    | The parameter value can be of any type.                                       |
| type | SQL data type. Valid values: `bigint`, `varchar`, `double`, `boolean`, `timestamp`, `decimal`, `array`, or `map`.</br>For the mappings between index and SQL data types, please see [Appendix: Data Type Mappings](#DataTypeMapping). |

### Return value type

The return value type is determined by the `type` parameter.

### Example

Parse the **remote_user** field value into a VARCHAR value:

```
* | select try_cast(remote_user as varchar)
```




<span id="DataTypeMapping"></span>
## Appendix: Data Type Mappings 

The mappings between index and SQL data types are as follows:

| Index Data Type | SQL Data Type |
| -------------- | ------------- |
| long           | bigint        |
| text           | varchar       |
| double         | double        |
| json           | varchar       |


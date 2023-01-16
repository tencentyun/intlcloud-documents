## Overview

String functions support string length calculation, case conversion, string concatenation, substring replacement, substring deletion, character locating, prefix/suffix matching, and more.
>! regular expression functions and string functions are for difference use cases. **Regular expression functions are more suitable for** extracting fields and field values from unstructured log data. For example, to extract `log_time` and `log_level` from logs, a regular expression function is more suitable.  
```
{
    “Log content”: "2021-12-02 14:33:35.022 [1] INFO  org.apache.Load - Response:status: 200, resp msg: OK, resp content: {    \"TxnId\": 58322,    \"Label\": \"flink_connector_20211202_1de749d8c80015a8\",    \"Status\": \"Success\",    \"Message\": \"OK\",    \"TotalRows\": 1,    \"LoadedRows\": 1,    \"FilteredRows\": 0,  \"CommitAndPublishTimeMs\": 16}"
}  
```
**String functions are more suitable for** processing the value of a specified field in structured log data such as following:
```
"resonsebody": {"method": "GET","user": "Tom"}
```

## Function str_count

#### Function definition

This function is used to search for a substring in a specified range of a value and return the number of occurrences of the substring.

#### Syntax description

```sql
str_count(Value, sub="", start=0, end=-1)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of string type |string| Yes | -  | -  |
|sub| Substring whose number of occurrences you want to count  |string| Yes | -  | -  |
|start| Start position to search |number| No | 0 | -  |
|end| End position to search |number| No | -1| -  |

#### Example
Raw log:
```
{"data": "warn,error,error"}
```
Processing rule:
```
fields_set("result", str_count(v("data"), sub="err"))
```
Processing result:
```
{"result":"2","data":"warn,error,error"}
```

## Function str_len

#### Function definition

This function is used to return the length of a string.

#### Syntax description

```sql
str_len(Value)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of string type |string| Yes | -  | -  |

#### Example

Raw log:
```
{"data": "warn,error,error"}
```
Processing rule:
```
fields_set("result", str_len(v("data")))
```
Processing result:
```
{"result":"16","data":"warn,error,error"}
```

## Function str_uppercase

#### Function definition

This function is used to convert a string to uppercase.

#### Syntax description

```sql
str_uppercase(Value)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of string type |string| Yes | -  | -  |

#### Example
Raw log:
```
{"data": "warn,error,error"}
```
Processing rule:
```
fields_set("result", str_uppercase(v("data")))
```
Processing result:
```
{"result":"WARN,ERROR,ERROR","data":"warn,error,error"}
```

## Function str_lowercase

#### Function definition

This function is used to convert a string to lowercase.

#### Syntax description

```sql
str_lowercase(Value)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of string type |string| Yes | -  | -  |

#### Example

Raw log:
```
fields_set("result", str_lowercase(v("data")))
```
Processing rule:
```
{"data": "WARN,ERROR,ERROR"}
```
Processing result:
```
{"result":"warn,error,error","data":"WARN,ERROR,ERROR"}
```

## Function str_join

#### Function definition

This function is used to concatenate input values by using a concatenation string.

#### Syntax description

```
str_join(Concatenation string 1, Value 1, Value 2, ...)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|join| Value of string type |string| Yes | -  | -  |
| Value parameter, list of variable parameters | Value of string type |string| Yes | -  | -  |

#### Example
Raw log:
```
{"data": "WARN,ERROR,ERROR"}
```
Processing rule:
```
fields_set("result", str_join(",", v("data"), "INFO"))
```
Processing result:
```
{"result":"WARN,ERROR,ERROR,INFO","data":"WARN,ERROR,ERROR"}
```

## Function str_replace

#### Function definition

This function is used to replace an old string with a new string.

#### Syntax description

```sql
str_replace(Value, old="", new="", count=0)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of string type |string| Yes | -  | -  |
|old| String to the replaced |string| Yes | - | - |
|new| Target string after replacement |string| Yes | - | - |
|count| Maximum replacement count. The default value is `0`, replacing all matched content. |number| No | 0 | - |

#### Example

Replace "WARN" in the value of the `data` field with "ERROR".

Raw log:
```
{"data": "WARN,ERROR,ERROR"}
```
Processing rule:
```
fields_set("result", str_replace( v("data"), old="WARN", new="ERROR"))
```
Save the replacement result to the new field `result`.
Processing result:
```
{"result":"ERROR,ERROR,ERROR","data":"WARN,ERROR,ERROR"}
```

## Function str_format

#### Function definition

This function is used to format strings.

#### Syntax description

```
str_format(Formatted string, Value 1, Value 2, ...)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|format| Target format, using "{}" as placeholders, such as "The disk \"{1}\" contains {0} file(s).". The numbers in "{}" correspond to the sequence numbers of the parameter values, and the numbers start from 0. For usage details, see [MessageFormat.format](https://docs.oracle.com/javase/7/docs/api/java/text/MessageFormat.html). |string| Yes | -  | -  |
| Value parameter, list of variable parameters | Value of string type |string| Yes | -  | -  |


#### Example

Raw log:
```
{"status": 200, "message":"OK"}
```
Processing rule:
```
fields_set("result", str_format("status:{0}, message:{1}", v("status"), v("message")))
```
Processing result:
```
{"result":"status:200, message:OK","message":"OK","status":"200"}
```

## Function str_strip

#### Function definition

This function is used to delete specified characters from a string concurrently from the start and end of the string and return the remaining part.

#### Syntax description

```
str_strip(Value, chars="\t\r\n")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of string type |string| Yes | -  | -  |
|chars| String to delete |string| No |\t\r\n| -  |


#### Example
- Example 1
Raw log:
```
{"data": " abc  "}
```
Processing rule:
```
fields_set("result", str_strip(v("data"), chars=" "))
```
Processing result:
```
{"result":"abc","data":" abc  "}
```
- Example 2
Raw log:
```
{"data": " **abc**  "}
```
Processing rule:
```
fields_set("result", str_strip(v("data"), chars=" *"))
```
Processing result:
```
{"result":"abc","data":" **abc**  "}
```

## Function str_lstrip

#### Function definition

This function is used to delete specified characters from a string from the start of the string and return the remaining part.

#### Syntax description

```sql
str_strip(Value, chars="\t\r\n")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of string type |string| Yes | -  | -  |
|chars| String to delete |string| No |\t\r\n| -  |


#### Example
Raw log:
```
{"data": " abc  "}
```
Processing rule:
```
fields_set("result", str_lstrip(v("data"), chars=" "))
```
Processing result:
```
{"result":"abc  ","data":" abc  "}
```

## Function str_rstrip

#### Function definition

This function is used to delete specified characters from a string from the end of the string and return the remaining part.

#### Syntax description

```sql
str_strip(Value, chars="\t\r\n")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of string type |string| Yes | -  | -  |
|chars| String to delete |string| No |\t\r\n| -  |

#### Example

Raw log:
```
{"data": " abc  "}
```
Processing rule:
```
fields_set("result", str_rstrip(v("data"), chars=" "))
```
Processing result:
```
{"result":" abc","data":" abc  "}
```

## Function str_find

#### Function definition

This function is used to check whether a string contains a specified substring and return the position of the substring in the string.

#### Syntax description

```sql
str_find(Value, sub="", start=0, end=-1)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of string type |string| Yes | -  | -  |
|sub| Substring whose number of occurrences you want to count  |string| Yes | -  | -  |
|start| Start position to search |number| No | 0 | -  |
|end| End position to search |number| No | -1| -  |


#### Example
Raw log:
```
{"data": "warn,error,error"}
```
Processing rule:
```
fields_set("result", str_find(v("data"), sub="err"))
```
Processing result:
```
{"result":"5","data":"warn,error,error"}
```

## Function str_start_with

#### Function definition

This function is used to check whether a string starts with a specified prefix.

#### Syntax description

```sql
str_start_with(Value, sub="", start=0, end=-1)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of string type |string| Yes | -  | -  |
|sub| Prefix string or character |string| Yes | -  | -  |
|start| Start position to search |number| No | 0 | -  |
|end| End position to search |number| No | -1| -  |


#### Example
- Example 1
Raw log:
```
{"data": "something"}
```
Processing rule:
```
fields_set("result", str_start_with(v("data"), sub="some"))
```
Processing result:
```
{"result":"true","data":"something"}
```
- Example 2
Raw log:
```
{"data": "something"}
```
Processing rule:
```
fields_set("result", str_start_with(v("data"), sub="*"))
```
Processing result:
```
{"result":"false","data":"something"}
```

## Function str_end_with

#### Function definition

This function is used to check whether a string starts with a specified prefix.

#### Syntax description

```
str_end_with(Value, sub="", start=0, end=-1)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of string type |string| Yes | -  | -  |
|sub| Prefix string or character |string| Yes | -  | -  |
|start| Start position to search |number| No | 0 | -  |
|end| End position to search |number| No | -1| -  |

#### Example

Raw log:
```
{"data": "endwith something"}
```
Processing rule:
```
fields_set("result", str_end_with(v("data"), sub="ing"))
```
Processing result:
```
{"result":"true","data":"endwith something"}
```

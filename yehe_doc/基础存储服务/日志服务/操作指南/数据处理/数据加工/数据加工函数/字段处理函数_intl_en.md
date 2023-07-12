## Overview

Field processing functions are used to process fields in logs. See the figure below.
![](https://qcloudimg.tencent-cloud.cn/raw/0bdc568ee0be67a3f1ddc438e96028ce.png)

## Function v

#### Function definition

This function is used to get the value of a specified field and return the corresponding string.

#### Syntax description

```sql
v(Field name)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| field | Field name  | string | Yes | -  | -  |

#### Example

Get the value of the "message" field and assign the value to a new field "new_message".

Raw log:
```
{"message": "failed", "status": "500"}
```
Processing rule:
```
fields_set("new_message", v("message"))
```
Processing result:
```
{"message": "failed", "new_message": "failed","status": "500"}
```


## Function fields_drop

#### Function definition

This function is used to delete the fields that meet a specified condition.

#### Syntax description

```sql
fields_drop(Field name 1, Field name 2, ..., regex=False,nest=False)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| Variable parameter, which can be a field name or regular expression of the field name | Variable parameter, which can be a field name or regular expression of the field name | string | Yes | -  | -  |
| regex | Whether to enable regular expression and use the full match mode | bool | No | False | -  |
| nest | Whether the field is a nested field | bool | No | False | -  |

#### Example

- Example 1. Delete the field whose name is "field"
Raw log:
```
{"field": "a,b,c", "status": "500"}
```
Processing rule:
```
fields_drop("field")
```
Processing result:
```
{"status":"500"}
```
- Example 2. Nested field processing
Raw log:
```
{"condition":"{\"a\":\"aaa\", \"c\":\"ccc\", \"e\":\"eee\"}","status":"500"}
```
Processing rule:
```
// `nest=True` indicates that the field is a nested field. After `condition.a` and `condition.c` are deleted, only the `condition.e` field is left.
t_if(if_json(v("condition")), fields_drop("condition.a", "condition.c", nest=True))
```
Processing result:
```
{"condition":"{\"e\":\"eee\"}","status":"500"}
```
- Example 3. Nested field processing
Raw log:
```
{"App": "thcomm","Message": "{\"f_httpstatus\": \"200\",\"f_requestId\": \"2021-11-09 08:40:17.832\tINFO\tservices/http_service.go:361\tbb20ac02-fcbc-4a56-b1f1-4064853b79da\",\"f_url\": \"wechat.wecity.qq.com/trpcapi/MbpsPaymentServer/scanCode\"}"}
```
Processing rule:
```
// `nest=True` indicates that the filed is a nested field. After `Message.f_requestId` and `Message.f_url` are deleted, only the `f_httpstatus` field is left.
t_if(if_json(v("Message")), fields_drop("Message.f_requestId", "Message.f_url", nest=True))
```
Processing result:
```
{"App":"thcomm","Message":"{\"f_httpstatus\":\"200\"}"}
```


## Function fields_keep

#### Function definition

This function is used to retain the fields that meet a specified condition.

#### Syntax description

```sql
fields_keep(Field name 1, Field name 2, ..., regex=False)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| Variable parameter, which can be a field name or regular expression of the field name | Variable parameter, which can be a field name or regular expression of the field name | string | Yes | -  | -  |
| regex | Whether to enable regular expression and use the full match mode | bool | No | False | -  |


#### Example

Retain the field whose name is "field" and delete the other fields.

Raw log:
```
{"field": "a,b,c", "status": "500"}
```
Processing rule:
```
fields_keep("field")
```
Processing result:
```
{"field":"a,b,c"}
```

## Function fields_pack

#### Function definition

This function is used to match field names based on a regular expression and encapsulate the matched fields into a new field whose value is in JSON format.

#### Syntax description

```sql
fields_pack(Target field name, include=".*", exclude="", drop_packed=False)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|output| Name of the new field after encapsulation |string| Yes | -  | -  |
|include| Regular expression to include the field name |string| No | -  | -  |
|exclude| Regular expression to exclude the field name |string| No | -  | -  |
|drop_packed| Whether to delete the original fields that are encapsulated |bool| No |False| -  |

#### Example
Raw log:
```
{"field_a": "a,b,c","field_b": "abc", "status": "500"}
```
Processing rule:
```
fields_pack("new_field","field.*", drop_packed=False)
```
Processing result:
```
{"new_field":"{\"field_a\":\"a,b,c\",\"field_b\":\"abc\"}","field_a":"a,b,c","field_b":"abc","status":"500"}
```


## Function fields_set

#### Function definition

This function is used to set field values or add fields.

#### Syntax description

```sql
fields_set(Field name 1, Field value 1, Field name 2, Field value 2, mode="overwrite")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| Variable parameter | List of key-value pairs |string| - | -  | -  |
|mode| Field overwrite mode |string| No |overwrite| - |


#### Example

- Example 1. Change the log level from Info to Waring
Raw log:
```
{"Level": "Info"}
```
Processing rule:
```
fields_set("Level", "Warning")
```
Processing result:
```
{"Level", "Warning"}
```
- Example 2. Add two fields: `new` and `new2`
Raw log:
```
{"a": "1", "b": "2", "c": "3"}
```
Processing rule:
```
fields_set("new", v("b"), "new2", v("c"))
```
Processing result:
```
{"a":"1","b":"2","c":"3","new":"2","new2":"3"}
```

## Function fields_rename

#### Function definition

This function is used to rename fields.

#### Syntax description

```sql
fields_rename(Field name 1, New field name 1, Field name 2, New field name 2, regex=False)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| Variable parameter | List of original-new field name pairs |string| - | - | - |
|regex| Whether to enable regular expression match for field names. If yes, use a regular expression to match the original field name. If no, use equal match. | bool | No | False | - |


#### Example
Raw log:
```
{"regieeen": "bj", "status": "500"}
```
Processing rule:
```
fields_rename("reg.*", "region", regex=True)
```
Processing result:
```
{"region":"bj","status":"500"}
```

## Function has_field

#### Function definition

If the specified field exists, the function returns `True`. Otherwise, the function returns `False`.

#### Syntax description

```sql
has_field(Field name)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| field | Field name | string | Yes | - | - |


#### Example

Raw log:
```
{"regiooon": "bj", "status": "500"}
```
Processing rule:
```
t_if(has_field("regiooon"), fields_rename("regiooon", "region"))
```
Processing result:
```
{"region":"bj","status":"500"}
```

## Function not_has_field  

#### Function definition

If the field does not exist, the function returns `True`. Otherwise, the function returns `False`.

#### Syntax description

```
not_has_field(Field name)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| field | Field name  | string | Yes | -  | -  |

#### Example

Raw log:
```
{"status": "500"}
```
Processing rule:
```
t_if(not_has_field("message"), fields_set("no_message", True))
```
Processing result:
```
{"no_message":"TRUE","status":"500"}
```


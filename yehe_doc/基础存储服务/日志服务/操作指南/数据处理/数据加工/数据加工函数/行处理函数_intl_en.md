## Overview

Row processing functions process log rows, such as filtering, distributing, and splitting log rows.
![](https://qcloudimg.tencent-cloud.cn/raw/1a08aacfadb7e606c4cc9864b0de84e9.png)

## Function log_output

#### Function definition

This function is used to output a row of log to a specified log topic. It can be used independently or together with branch conditions.

#### Syntax description

log_output(Alias). The alias is defined when the processing task is configured.

#### Field description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| alias | Log topic alias | string | Yes | -   | -   |

#### Sample

Distribute the log to 3 different log topics according to the values (`waring`, `info`, and `error`) of the `loglevel` field.

Raw log:
```
[
  {
    "loglevel": "warning"
  },
  {
    "loglevel": "info"
  },
  {
    "loglevel": "error"
  }
]
```
Processing rule:
```
// The `loglevel` field has 3 values (`waring`, `info`, and `error`) and therefore the log is distributed to 3 different log topics accordingly.
t_switch(regex_match(v("loglevel"),regex="info"),log_output("info_log"),regex_match(v("loglevel"),regex="warning"),log_output("warning_log"),regex_match(v("loglevel"),regex="error"),log_output("error_log"))
```




## Function log_split

#### Function definition

This function is used to split a row of log into multiple rows of logs based on the value of a specified field by using a separator and JMES expression.

#### Syntax description

```sql
log_split(Field name, sep=",", quote="\"", jmes="", output="")
```

#### Field description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| field | Field to extract | string | Yes   | -       | -      |
| sep | Separator | string | No | , | Any single character |
| quote    | Characters that enclose the value    | string            | No            | -           | -              |
| jmes        | JMES expression. For more information, see [JMESPath](https://jmespath.org/).                      | string | No   | -          | -     |
| output  | Name of a single field  |string  | Yes  | -  | -  |

#### Sample

- Example 1. Split a log whose `field` has multiple values
```
{"field": "hello Go,hello Java,hello python","status":"500"}
```
Processing rule:
```
// Use the separator "," to split the log into 3 logs.
log_split("field", sep=",",  output="new_field")
```
Processing result:
```
{"new_field":"hello Go","status":"500"}
{"new_field":"hello Java","status":"500"}
{"new_field":"hello python","status":"500"}
```
- Example 2. Use a JMES expression to split a log
```
{"field": "{\"a\":{\"b\":{\"c\":{\"d\":\"a,b,c\"}}}}", "status": "500"}
```
Processing rule:
```
// The value of `a.b.c.d` is `a,b,c`.
log_split("field", jmes="a.b.c.d",  output="new_field")
```
Processing result:
```
{"new_field":"a","status":"500"}
{"new_field":"b","status":"500"}
{"new_field":"c","status":"500"}
```
- Example 3. Split a log that contains a JSON array
```
{"field": "{\"a\":{\"b\":{\"c\":{\"d\":[\"a\",\"b\",\"c\"]}}}}", "status": "500"}
```
Processing rule:
```
log_split("field", jmes="a.b.c.d",  output="new_field")
```
Processing result:
```
{"new_field":"a","status":"500"}
{"new_field":"b","status":"500"}
{"new_field":"c","status":"500"}
```


## Function log_drop

#### Function definition

This function is used to delete logs that meet a specified condition.

#### Syntax description

```sql
log_drop(Condition 1)
```

#### Field description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|condition  | Function expression whose return value is of bool type  | bool  |  Yes  | - | -  |


#### Sample

Delete logs where `status` is `200` and retain other logs.

Raw log:
```
{"field": "a,b,c", "status": "500"}
{"field": "a,b,c", "status": "200"}
```
Processing rule:
```
log_drop(op_eq(v("status"), 200))
```
Processing result:
```
{"field":"a,b,c","status":"500"}
```


## Function log_keep

#### Function definition

This function is used to retain logs that meet a specified condition.

#### Syntax description

```sql
log_keep(Condition 1)
```

#### Field description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|condition  | Function expression whose return value is of bool type  | bool  |  Yes  | - | -  |


#### Sample

Retain logs where `status` is `500` and delete other logs.

Raw log:
```
{"field": "a,b,c", "status": "500"}
{"field": "a,b,c", "status": "200"}
```
Processing rule:
```
log_keep(op_eq(v("status"), 500))
```
Processing result:
```
{"field":"a,b,c","status":"500"}
```

## Function log_split_jsonarray_jmes

#### Function definition

This function is used to split and expand the JSON array in the log according to JMES syntax.

#### Syntax description

```sql
log_split_jsonarray_jmes("field", jmes="items", prefix="")
```

#### Field description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| field | Field to extract | string | Yes | -  | -  |

#### Sample

- Example 1
Raw log:
```
{"common":"common","result":"{\"target\":[{\"a\":\"a\"},{\"b\":\"b\"}]}"}
```
Processing rule:
```
log_split_jsonarray_jmes("result",jmes="target")
fields_drop("result")
```
Processing result:
```
{"common":"common", "a":"a"}
{"common":"common", "b":"b"}
```
- Example 2
Raw log:
```
{"common":"common","target":"[{\"a\":\"a\"},{\"b\":\"b\"}]"}
```
Processing rule:
```
log_split_jsonarray_jmes("target",prefix="prefix_")
fields_drop("target")
```
Processing result:
```
{"prefix_a":"a", "common":"common"}
{"prefix_b":"b", "common":"common"}
```



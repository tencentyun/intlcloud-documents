## Overview

Row processing functions process log rows, such as filtering, distributing, and splitting log rows.
![](https://qcloudimg.tencent-cloud.cn/raw/1a08aacfadb7e606c4cc9864b0de84e9.png)

## Function log_output

#### Function definition

This function is used to output a row of log to a specified log topic. It can be used independently or together with branch conditions.

#### Syntax description

log_output(Alias) (The alias is defined during processing task configuration, as shown in the figure below.)
![](https://qcloudimg.tencent-cloud.cn/raw/0c4e3f2d99257c6f8e607b56798e04db.jpg)

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| alias | Log topic alias | string | Yes | -   | -   |

#### Example

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
Processing result:
![](https://qcloudimg.tencent-cloud.cn/raw/0e99dd62ca4f13f4d5260310ad4a2648.jpg)


## Function log_split

#### Function definition

This function is used to split a row of log into multiple rows of logs based on the value of a specified field by using a separator and JMES expression.

#### Syntax description

```sql
log_split(Field name, sep=",", quote="\"", jmes="", output="")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| field | Field to extract | string | Yes   | -       | -      |
| sep | Separator | string | No | , | Any single character |
| quote    | Characters that enclose the value    | string            | No            | -           | -              |
| jmes        | JMES expression. For more information, see [JMESPath](https://jmespath.org/).                      | string | No   | -          | -     |
| output  | Name of a single field  |string  | Yes  | -  | -  |

#### Example

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

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|condition  | Function expression whose return value is of bool type  | bool  |  Yes  | - | -  |


#### Example

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

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|condition  | Function expression whose return value is of bool type  | bool  |  Yes  | - | -  |


#### Example

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


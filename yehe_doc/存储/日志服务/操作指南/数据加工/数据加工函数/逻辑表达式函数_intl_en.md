## Overview

Logic and arithmetic functions include AND, OR, greater than, less than, equal to, addition, subtraction, multiplication, division, and modulus operation functions. Their writing method is slightly different from that of commonly used programming languages, as shown in the figure below.
![](https://qcloudimg.tencent-cloud.cn/raw/293f6c206aeef96d8b8c4dcabd37d3da.jpg)

## Function op_if

#### Function definition

This function is used to return a value based on a specified condition.

#### Syntax description

```sql
op_if(Condition 1, Value 1, Value 2)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|condition|Condition expression|bool|Yes|-|-|
|data1| If the condition is `True`, the value of this parameter is returned. |string| Yes |-|-|
|data2| If the condition is `False`, the value of this parameter is returned. |string| Yes |-|-|

#### Examples
- Example 1
Raw log:
```
{"data": "abc"}
```
Processing rule:
```
fields_set("result", op_if(True, v("data"), "false"))
```
Processing result:
```
{"result":"abc","data":"abc"}
```
- Example 2
Raw log:
```
{"data": "abc"}
```
Processing rule:
```
fields_set("result", op_if(False, v("data"), "123"))
```
Processing result:
```
{"result":"123","data":"abc"}
```

## Function op_ifnull

#### Function definition

This function is used to return the first non-null and non-empty result value.

#### Syntax description

```SQL

op_ifnull(Value 1, Value 2, ...)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| Variable parameter list | Parameters or expressions that participate in the calculation |string| Yes |-|-|

#### Examples
Raw log:
```
{"data1": null, "data2": "", "data3": "first not null"}
```
Processing rule:
```
fields_set("result", op_ifnull(v("data1"), v("data2"), v("data3")))
```
Processing result:
```
{"result":"first not null","data3":"first not null","data2":"","data1":"null"}
```


## Function op_and

#### Function definition

This function is used to perform the AND operation on values. If all the specified parameter values are evaluated to true, `True` is returned. Otherwise, `False` is returned.

#### Syntax description

```sql
op_and(Value 1, Value 2, ...)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| Variable parameter list | Parameters or expressions that participate in the calculation |string| Yes |-|-|


#### Examples
- Example 1
Raw log:
```
{}
```
Processing rule:
```
fields_set("result", op_and(True, False))
```
Processing result:
```
{"result":"false"}
```
- Example 2
Raw log:
```
{}
```
Processing rule:
```
fields_set("result", op_and(1, 1))
```
Processing result:
```
{"result":"true"}
```
- Example 3
Raw log:
```
{"data":"false"}
```
Processing rule:
```
fields_set("result", op_and(1, v("data")))
```
Processing result:
```
{"result":"false","data":"false"}
```

## Function op_or

#### Function definition

This function is used to perform the OR operation on values. If one or more of the specified parameter values are evaluated to false, `False` is returned. Otherwise, `True` is returned.

#### Syntax description

```sql
op_or(Value 1, Value 2, ...)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| Variable parameter list | Parameters or expressions that participate in the calculation |string| Yes |-|-|

#### Examples
Raw log:
```
{}
```
Processing rule:
```
fields_set("result", op_or(True, False))
```
Processing result:
```
{"result":"true"}
```


## Function op_not

#### Function definition

This function is used to perform the NOT operation on values.

#### Syntax description

```sql
op_not(Value)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Value of any type |any| Yes |-|-|


#### Examples
- Example 1
Raw log:
```
{}
```
Processing rule:
```
fields_set("result", op_not(True))
```
Processing result:
```
{"result":"false"}
```
- Example 2
Raw log:
```
{}
```
Processing rule:
```
fields_set("result", op_not("True"))
```
Processing result:
```
{"result":"false"}
```

## Function op_eq

#### Function definition

This function is used to compare two values. If the values are equal, `True` is returned.

#### Syntax description

```sql
op_eq(Value 1, Value 2)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| data1 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |
| data2 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |

#### Examples
- Example 1. Determine whether the values of the `Post` and `Get` fields are equal
Raw log:
```
{"Post": "10", "Get": "11"}
```
Processing rule:
```
fields_set("result", op_eq(v("Post"), v("Get")))
```
Save the result to `result`.
Processing result:
```
{"result":"false","Post":"10","Get":"11"}
```
- Example 2. Determine whether the values of the `field1` and `field2` fields are equal
Raw log:
```
{"field1": "1", "field2": "1"}
```
Processing rule:
```
fields_set("result", op_eq(v("field1"), v("field2")))
```
Processing result:
```
{"result":"true","field1":"1","field2":"1"}
```

## Function op_ge

#### Function definition

This function is used to compare two values. If `Value 1` is greater than or equal to `Value 2`, `True` is returned.

#### Syntax description

```sql
op_ge(Value 1, Value 2)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| data1 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |
| data2 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |


#### Examples
- Example 1
Raw log:
```
{"field1": "20", "field2": "9"}
```
Processing rule:
```
fields_set("result", op_ge(v("field1"), v("field2")))
```
Processing result:
```
{"result":"true","field1":"20","field2":"9"}
```
- Example 2
Raw log:
```
{"field1": "2", "field2": "2"}
```
Processing rule:
```
fields_set("result", op_ge(v("field1"), v("field2")))
```
Processing result:
```
{"result":"true","field1":"2","field2":"2"}
```

## Function op_gt

#### Function definition

This function is used to compare two values. If `Value 1` is greater than `Value 2`, `True` is returned.

#### Syntax description

```sql
op_gt(Value 1, Value 2)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| data1 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |
| data2 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |

#### Examples
Raw log:
```
{"field1": "20", "field2": "9"}
```
Processing rule:
```
fields_set("result", op_ge(v("field1"), v("field2")))
```
Processing result:
```
{"result":"true","field1":"20","field2":"9"}
```


## Function op_le

#### Function definition

This function is used to compare two values. If `Value 1` is less than or equal to `Value 2`, `True` is returned.

#### Syntax description

```sql
op_le(Value 1, Value 2)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| data1 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |
| data2 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |


#### Examples
Raw log:
```
{"field1": "2", "field2": "2"}
```
Processing rule:
```
fields_set("result", op_le(v("field1"), v("field2")))
```
Processing result:
```
{"result":"true","field1":"2","field2":"2"}
```

## Function op_lt

#### Function definition

This function is used to compare two values. If `Value 1` is less than `Value 2`, `True` is returned.

#### Syntax description

```sql
op_lt(Value 1, Value 2)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| data1 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |
| data2 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |


#### Examples
Raw log:
```
{"field1": "2", "field2": "3"}
```
Processing rule:
```
fields_set("result", op_lt(v("field1"), v("field2")))
```
Processing result:
```
{"result":"true","field1":"2","field2":"3"}
```

## Function op_add

#### Function definition

This function is used to return the sum of two specified values.

#### Syntax description

```sql
op_add(Value 1, Value 2)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| data1 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |
| data2 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |

#### Examples
Raw log:
```
{"field1": "1", "field2": "2"}
```
Processing rule:
```
fields_set("result", op_add(v("field1"), v("field2")))
```
Processing result:
```
{"result":"3","field1":"1","field2":"2"}
```


## Function op_sub

#### Function definition

This function is used to return the difference between two specified values.

#### Syntax description

op_sub(Value 1, Value 2)

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| data1 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |
| data2 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |

#### Examples
Raw log:
```
{"field1": "1", "field2": "2"}
```
Processing rule:
```
fields_set("result", op_sub(v("field1"), v("field2")))
```
Processing result:
```
{"result":"-1","field1":"1","field2":"2"}
```


## Function op_mul

#### Function definition

This function is used to return the product of two specified values.

#### Syntax description

```sql
op_mul(Value 1, Value 2)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| data1 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |
| data2 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |

#### Examples
Raw log:
```
{"field1": "1", "field2": "2"}
```
Processing rule:
```
fields_set("result", op_mul(v("field1"), v("field2")))
```
Processing result:
```
{"result":"2","field1":"1","field2":"2"}
```


## Function op_div

#### Function definition

This function is used to return the quotient of two specified values.

#### Syntax description

```sql
op_div(Value 1, Value 2)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| data1 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |
| data2 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |


#### Examples
- Example 1
Raw log:
```
{"field1": "1", "field2": "2"}
```
Processing rule:
```
fields_set("result", op_div(v("field1"), v("field2")))
```
Processing result:
```
{"result":"0","field1":"1","field2":"2"}
```
- Example 2
Raw log:
```
{"field1": "1.0", "field2": "2"}
```
Processing rule:
```
fields_set("result", op_div(v("field1"), v("field2")))
```
Processing result:
```
{"result":"0.5","field1":"1.0","field2":"2"}
```

## Function op_sum

#### Function definition

This function is used to return the sum of multiple specified values.

#### Syntax description

```sql
op_sum(Value 1, Value 2, ...)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| Variable parameter list | Numeric value or string that can be converted to a numeric value |string| Yes |-|-|

#### Examples
Raw log:
```
{"field1": "1.0", "field2": "10"}
```
Processing rule:
```
fields_set("result", op_sum(v("field1"), v("field2")))
```
Processing result:
```
{"result":"11.0","field1":"1.0","field2":"10"}
```


## Function op_mod

#### Function definition

This function is used to return the remainder of a specified value divided by the other specified value.

#### Syntax description

```sql
op_mod(Value 1, Value 2)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
| data1 | Numeric value or string that can be converted to a numeric value |number| Yes | - | - |

#### Examples
- Example 1
Raw log:
```
{"field1": "1.0", "field2": "0"}
```
Processing rule:
```
fields_set("result", op_mod(v("field1"), v("field2")))
```
Processing result:
```
{"result":"2","field1":"1","field2":"2"}
```
- Example 2
Raw log:
```
{"field1": "1.0", "field2": "5"}
```
Processing rule:
```
fields_set("result", op_mod(v("field1"), v("field2")))
```
Processing result:
```
{"result":"1.0","field1":"1.0","field2":"5"}
```
- Example 3
Raw log:
```
{"field1": "6", "field2": "4"}
```
Processing rule:
```
fields_set("result", op_mod(v("field1"), v("field2")))
```
Processing result:
```
{"result":"2","field1":"6","field2":"4"}
```

## Overview

The functions below can be used to convert common field values to the int, float, bool, and str types.

## Function ct_int

#### Function definition

This function is used to convert a value (whose base can be specified) to a decimal integer.

#### Syntax description

```sql
ct_int(Value 1, base=10)
```


#### Parameter description
| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Numeric value or string that can be converted to a numeric value |number| Yes | -  | -  |
|base| Base |number| No | 10 |[2-36]|

#### Examples

- Example 1
Raw log:
```
{"field1": "10"}
```
Processing rule:
```
fields_set("result", ct_int(v("field1")))
```
Processing result:
```
{"result":"10","field1":"10"}
```
- Example 2
Raw log:
```
{"field1": "AB"}
```
Processing rule:
```
fields_set("result", ct_int(v("field1"), 16))
```
Processing result:
```
{"result":"171","field1":"AB"}
```

## Function ct_float

#### Function definition

This function is used to convert a value to a floating-point number.

#### Syntax description

```sql
ct_float(Value)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Numeric value or string that can be converted to a numeric value |number| Yes | -  | -  |


#### Examples
Raw log:
```
{"field1": "123"}
```
Processing rule:
```
fields_set("result", ct_float(v("field1")))
```
Processing result:
```
{"result":"123.0","field1":"123"}
```

## Function ct_str

#### Function definition

This function is used to convert a value to a string.

#### Syntax description

```sql
ct_str(Value)
```

#### Parameter description
| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Numeric value or string that can be converted to a numeric value |number| Yes | -  | -  |

#### Examples

Raw log:
```
{"field1": 123}
```
Processing rule:
```
fields_set("result", ct_str(v("field1")))
```
Processing result:
```
{"result":"123","field1":"123"}
```

## Function ct_bool

#### Function definition

This function is used to convert a value to a Boolean value.

#### Syntax description

```sql
ct_bool(Value)
```

#### Parameter description

| Parameter | Description | Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Numeric value or string that can be converted to a numeric value |number| Yes | -  | -  |

#### Examples
- Example 1
Raw log:
```
{}
```
Processing rule:
```
fields_set("result", ct_bool(0))
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
fields_set("result", ct_bool(1))
```
Processing result:
```
{"result":"true"}
```
- Example 3
Raw log:
```
{"field1": 1}
```
Processing rule:
```
fields_set("result", ct_bool(v("field1")))
```
Processing result:
```
{"result":"true","field1":"1"}
```

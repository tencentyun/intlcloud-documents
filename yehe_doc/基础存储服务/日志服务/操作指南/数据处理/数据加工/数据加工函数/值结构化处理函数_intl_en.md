## Overview

Value structuring functions can be used to extract values of specified JSON nodes, convert XML data to JSON data and vice versa, and determine whether a value is a JSON string.

## Function json_select

#### Function definition

This function is used to extract a JSON field value with a JMES expression and return the JSON string of the extraction result.

#### Syntax description

```sql
json_select(v(Field name), jmes="")
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value, which can be extracted by other functions |string| Yes| -  | -  |
|jmes| JMES expression |string|Yes| -  | -  |

#### Example

Raw log:
```
{"field": "{\"a\":{\"b\":{\"c\":{\"d\":\"success\"}}}}", "status": "500"}
```
Processing rule:
```
fields_set("message", json_select(v("field"), jmes="a.b.c.d"))
```
Processing result:
```
{"field":"{\"a\":{\"b\":{\"c\":{\"d\":\"success\"}}}}","message":"success","status":"500"}
```


## Function xml_to_json

#### Function definition

This function is used to parse and convert an XML-formatted value to a JSON string. The input value must be an XML string. Otherwise, a conversion exception will occur.

#### Syntax description

```sql
xml_to_json(Field value)
```

#### Parameter description
| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value |string|Yes| -  | -  |


#### Example

Raw log:
```
{"xml_field": "<note><to>B</to><from>A</from><heading>Reminder</heading><body>Don't forget me this weekend!</body></note>", "status": "500"}
```
Processing rule:
```
fields_set("json_field", xml_to_json(v("xml_field")))
```
Processing result:
```
{"xml_field":"<note><to>B</to><from>A</from><heading>Reminder</heading><body>Don't forget me this weekend!</body></note>","json_field":"{\"to\":\"B\",\"from\":\"A\",\"heading\":\"Reminder\",\"body\":\"Don't forget me this weekend!\"}","status":"500"}
```


## Function json_to_xml 

#### Function definition

This function is used to parse and convert a JSON string value to an XML string.

#### Syntax description

```sql
json_to_xml(Field value)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value |string|Yes| -  | -  |

#### Example

Raw log:
```
{"json_field":"{\"to\":\"B\",\"from\":\"A\",\"heading\":\"Reminder\",\"body\":\"Don't forget me this weekend!\"}", "status": "200"}
```
Processing rule:
```
fields_set("xml_field", json_to_xml(v("json_field")))
```
Processing result:
```
{"json_field":"{\"to\":\"B\",\"from\":\"A\",\"heading\":\"Reminder\",\"body\":\"Don't forget me this weekend!\"}","xml_field":"<ObjectNode><to>B</to><from>A</from><heading>Reminder</heading><body>Don't forget me this weekend!</body></ObjectNode>","status":"200"}
```


## Function if_json

#### Function definition

This function is used to determine whether a value is a JSON string.

#### Syntax description

```sql
if_json(Field value)
```

#### Parameter description

| Parameter | Description | Parameter Type | Required | Default Value | Value Range |
|----------- | ----------- | ----------- | ----------- | -------------- | -------------- |
|data| Field value |string|Yes| -  | -  |

#### Example
- Example 1
Raw log:
```
{"condition":"{\"a\":\"b\"}","status":"500"}
```
Processing statement:
```
t_if(if_json(v("condition")), fields_set("new", 1))
```
Processing result:
```
{"new":"1","condition":"{\"a\":\"b\"}","status":"500"}
```
- Example 2
Raw log:
```
{"condition":"haha","status":"500"}
```
Processing statement:
```
t_if(if_json(v("condition")), fields_set("new", 1))
```
Processing result:
```
{"condition":"haha","status":"500"}
```

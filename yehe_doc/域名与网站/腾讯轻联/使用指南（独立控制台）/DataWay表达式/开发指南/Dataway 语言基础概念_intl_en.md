This document describes the core concepts and features of Dataway. Dataway is a scripting engine for custom data conversion and processing in iPaaS. You can use it to write and execute powerful and complex data conversion scripts.

## Dataway Toolset
Dataway provides three script toolset modes: text, expression, and code modes, which support distinctive semantics and syntax to meet the data requirements in different use cases. The textboxes of Dataway support all the three toolsets (certain toolsets are disabled for certain components due to the feature design). You can select one to enter the script based on your application needs and habits.

| Mode | Purpose | Description |
|---------|---------|---------|
| Text mode | Data creation and transfer. | You can generate the required data or reference the context data of a flow as instructed on the GUI. |
| <nobr>Expression mode</nobr> | Simple data conversion and processing as well as lightweight script execution. | You can enter an expression to get the required data. |
| Code mode | Complex data conversion and processing as well as complex script execution, formatting, and debugging. | You can write a complete Python 3 or Java JDK 8 script to get the required data. |

The **flow data panel** embeds all the three modes to reference the context data of a flow. You can click data in the previous components to quickly reference it.


[](id:core-types)
## Dataway Type System

 Dataway has the following core types, which can be used as the output results of Dataway scripts to be passed between components:

| Type | Name | Description | Unique to Dataway | Example |
| ------------------------------- | ---------- | ------------------------------------------------------------ | --------------------- | ------------------------------------------------------------ |
| None                            | Null | Null.                                                     | No                    | Python: None; Java: null                                    |
| string                          | String     | String.                                                   | No                    | "abc"                                                        |
| bytes                           | Byte array   | Byte array.                                                 | No                    | Python: b"abc"; Java: "abc".getBytes()                      |
| bool                            | Boolean     | Boolean.                                                    | No                    | Python: True/False; Java: true/false                        |
| float                           | Float     | Float.                                                     | No                    | 123.456                                                      |
| int/Long                        | Integer       | Integer.                                                         | No                    | Python: 123; Java: 123L                                     |
| list                            | List       | Sequence container.                                                 | No                    | Python: [1,2,3]; Java: new java.util.ArrayList<>()          |
| dict/Map                        | Dictionary       | Key-value container.                                                 | No                    | Python: {1:1, 'key': 'value'}; Java: new java.util.HashMap<>() |
| decimal                         | Decimal     | It is used for accurate decimal value calculation.                                       | No                    | Python: decimal.Decimal(1); Java: new java.math.BigDecimal("1") |
| datetime                        | Date and time       | Date and time.                                         | No                    | Python: datetime.datetime.now(); Java: java.time.OffsetDateTime.now() |
| date                            | Date       | Date.                                                         | No                    | Python: datetime.date.today(); Java: java.time.LocalDate.now() |
| time                            | Time       | Time.                                                         | No                    | Python: datetime.datetime.now().time(); Java: java.time.OffsetTime.now() |
| [**Entity**](#entity-explain)   | Binary entity | Entity data in iPaaS, which represents a binary object, including `blob`, `mime_type`, and `encoding`. | Yes                    | `payload` in a message constructed by the HTTP Listener component                           |
| **MultiMap**                    | Multi-value dictionary   | Like `xml` but unlike `dict`, this type supports duplicate `key` values.          | Yes                    | Object obtained after data in `application/www-form-urlencoded` format is parsed |
| **FormDataParts**               | Form data   | Array + list data structure, which is similar to `orderDict` in Python.       | Yes                    | Object obtained after data in `multipart/form-data` format is parsed               |
| [**Message**](#message-explain) | Message       | Message in iPaaS, which carries flow data, including `payload`, `variables`, and `attributes`. | Yes                    | `msg` parameter in the `dw_process` entry function in a script in Python code mode        |
| **DataSet**                     | Dataset     | Dataset in iPaaS data integration, which can be manipulated through the data integration component.             | Yes                    | Output of the Builder component                                           |
| **Record**                      | Single data record   | Single data record in iPaaS data integration, which contains the schema.                  | Yes                    | It can be obtained by using the Foreach component to traverse `DataSet`                         |

Core types in Dataway are available in all the three script toolsets and have the corresponding data structures. Although the operation method of different data structures of the same type varies by script toolset, you can still convert data structures losslessly while ensuring that the core characteristics of different same-type data structures are the same.
If different script toolsets are used upstream and downstream of a flow, different data structures of the same type can be automatically mapped in an imperceptible manner. You can use different Dataway script toolsets in different Dataway textboxes, which will not affect the consistency and accuracy of processing of data of core types.

>!If the output result of a Dataway script is the final result returned by the flow, the types supported for the returned value will also be subject to the flow components. If an HTTP Listener component is used as a trigger in the flow, the final returned value must be of the `Entity` type.

In addition to the core types, each script toolset also supports certain unique types. However, **data of the unique types cannot be used as the output result of Dataway scripts**; otherwise, an error will occur. For more information, see Text Mode, Expression Mode, Python Code Mode, and Java Code Mode.


[](id:message-explain)
## `Message` Type

In Dataway, the `Message` type carries an iPaaS message, which will be passed and updated during flow execution. The `Message` type contains attributes such as `payload`, `vars`, and `attrs`, which are collectively called **predefined attributes**. These attributes are generated by the system based on the current execution information and processed data and used to get the flow context information in a Dataway script.

>?The input of a Dataway script is the `msg` variable, which is of `Message` type and carries the context information of the flow for execution previous to the current component node.

The attributes in the `Message` type are as detailed below:

| Attribute | How to get (Python code mode example) | Description | Type | Remarks |
| ----- | --- | ------- | -------- | ----- |
| Variable set | msg.vars | Variable set in the context of the current message. | Dictionary type: The key is of the string type and represents the variable name; the value is of any [core type](#core-types) and represents the variable value. | The set variables are shared among all subsequent component nodes in the flow. Therefore, this attribute can be used for data integration between different component nodes. |
| Payload | msg.payload | Payload data of the current message. | Any [core type](#core-types) | `payload` is the payload data in an iPaaS message, which represents the execution result of a component node. It will be updated after a node is executed and can be configured through certain components such as **Set Payload**. For example, the HTTP Listener component will construct the payload content based on the received network request, so the payload will be of `Entity` type after being processed by an HTTP Listener component. |
| Attribute set | msg.attrs | A set of attributes of the current message, including message source and headers. | Dictionary type: The key is of the string type and represents the attribute name; the value is of any [core type](#core-types) and represents the attribute value. | If the flow trigger is HTTP Listener, the network request headers will be stored in `msg.attrs`. |
| Unique ID | msg.id | The unique ID of the current message. | String type | The unique ID may change after the message passes a logical component. |
| Sequence number | msg.seq_id | The sequence number of the current message. | String type | The sequence number keeps unchanged when the message is transferred in a flow. |
| Error message | msg.error | Error message in the context of the currently processed context. | Dictionary type: The key is of the string type and represents the error attribute name; the value is of the string type and represents the attribute value. | It contains `code` (error type) and `desc` (error description string). |


[](id:entity-explain)
## `Entity` Type

### Overview

In Dataway, the `Entity` type carries the entity data of iPaaS and is an encapsulation object of binary data. It contains the **raw data (`blob`)**, **MIME type (`mime_type`)**, and **encoding type (`encoding`)**.

- **Raw data (`blob`)**: Raw binary data.
- **MIME type (`mime_type`)**: Content format of binary data, such as `application/json`, `application/www-form-urlencoded`, and `multipart/form-data`.
- **Encoding type (`encoding`)**: String encoding type of binary data, such as `utf8` and `gbk`.

You can access content in `Entity` as follows (taking the Python code mode as an example):

| Access Method | Description |
|---------|---------|
| entity['^blob'] | Gets the payload data of the binary object. A `bytes` object will be returned. |
| entity['^mime_type'] | Gets the MIME type of the message object. A string object will be returned. |
| entity['^encoding'] | Gets the encoding type of the message object. A string object will be returned. |


For ease of use, Dataway also provides object methods such as `entity.get(attr, default=None)` and subscript-based selector syntax (for more information, see [`Entity` selector](#selectors)) for quick access:
- entity\['^value'\]: Parses the payload data based on the MIME and encoding types and returns the parsing result, which is of a [core type](#core-types).
- entity\['xxxx'\]: Parses the payload data based on the MIME and encoding types and returns the value of the specified key, which is equivalent to `entity\['^value'\]['xxx']`.
- entity.get(attr, default=None): Parses the payload data based on the MIME and encoding types and returns the value of the specified key. If no value can be obtained, the default value (`None` by default) will be returned. This syntax is equivalent to `entity['^value'].get(attr, default=None)`.

When you use the quick access feature, the system will try parsing the binary payload data in `Entity`. If parsing fails, a runtime error will occur. For more information, see [Supported MIME Types](#mime-type).


[](id:selectors)
### `Entity` selector

For common MIME and encoding types, Dataway allows you to use a selector to quickly access the content in an `Entity` object. The following operation types are supported:

| Subscript Type | Description | Example |
| ---------------------------------------- | -------------------------------------------------------------------------------- | ------------------------- |
| Number | Used to access the ith element in the current array. | entity[0]            |
| String starting with `^` | Used to get the metadata such as `^mime_type`, `^encoding`, `^blob` (raw binary data), and `^value`. | entity['^mime_type'] |
| Common character (letter, digit, underscore, hyphen, or dot) | A common character key, which is used to get a sub-element of the current element by name. If there are multiple sub-elements with the same name, only the first one will be returned. | entity['list']     |

Below are examples of the above selector types. Suppose `msg.payload` of the input message is an `Entity` object, and its raw data `blob` is parsed into a JSON array, MIME type is `application/json`, and encoding type is `utf-8`.
```json
 [{"a1":1},{"b1":1,"b2":2,"b3":3},{"c1":[1,2,3]}] 
```


#### Example 1: Use a number subscript to get the data

You can use a number script to get an element in `msg.payload`. Below is a sample Dataway expression:
```python
def dw_process(msg):
    return msg.payload[1]
```
The expression output will be of `dict` type: `{"b1":1,"b2":2,"b3":3}`.

#### Example 2: Use the `^` symbol to get the metadata

You can use the `^` symbol to get the metadata in `msg.payload`. Below is a sample Dataway expression:
```python
def dw_process(msg):
    return {
        "mimeType" : msg.payload["^mime_type"],
        "encoding": msg.payload["^encoding"],
        "blob": msg.payload["^blob"],
        "value": msg.payload["^value"],
    }
```
The expression output will be of `dict` type:
```python
{
    "mimeType" : "application/json",
    "encoding": "utf-8",
    "blob": b'[{"a1":1},{"b1":1,"b2":2,"b3":3},{"c1":[1,2,3]}]',
    "value": [{"a1":1},{"b1":1,"b2":2,"b3":3},{"c1":[1,2,3]}]
}
```


#### Example 3: Use common characters to get elements
Suppose the value of `msg.payload` is still of `Entity` type, the MIME and encoding types are still `application/json` and `utf-8` respectively, but the payload data `blob` is parsed into the following:
```json
{"a1":1,"b1":1,"b2":2,"b3":3,"c1":[1,2,3]}
```
If the following Dataway expression is used:
```python
def dw_process(msg):
    return {
        "a1" : msg.payload["a1"],
        "b2": msg.payload["b2"],
        "c1": msg.payload['c1'],
    }
```
The expression output will be of `dict` type:
```python
{
    "a1" : 1,
    "b2": 2,
    "c1": [1,2,3]
}
```


### `Entity` object construction (Python code mode example)
[](id:from-value)
#### 1. Value-based constructor (`Entity.from_value`)
This method is used to encapsulate `data` into an `Entity` object and return it as follows:
```python
Entity.from_value(data, mime_type=None, encoding="utf-8")
```
 `Entity.from_value` serializes `data` based on the specified MIME and encoding types to get the raw data of `bytes` type, encapsulates it into an `Entity` object, and returns the object.
    
    Here, the `mime_type` parameter is required. Currently, six MIME types are supported: `text/plain`, `application/json` (the alias is `text/json`), `application/x-www-form-urlencoded`, `application/csv`, `application/xml` (the alias is `text/xml`), and `multipart/form-data`; the `encoding` parameter can be any valid encoding type and will be `utf-8` by default if it is left empty.

[](id:from-bytes)
#### 2. Raw data-based constructor (`Entity.from_bytes`) 
This method is used to encapsulate a string or a `bytes` object into an `Entity` object and return it as follows:
```python
Entity.from_bytes(data, mime_type=None, encoding="utf-8")
```
  The verification rules of the `mime_type` and `encoding` parameters in `Entity.from_bytes` are similar to those in `Entity.from_value` but differ in that the `mime_type` value is not limited and can be any MIME type.
    
  If the `data` parameter passed to the `Entity.from_bytes` method is of `bytes` type, the method will directly return an `Entity` object with the raw data of `data`, MIME type of `mime_type`, and encoding type of `encoding`.
  If the passed `data` parameter is a string, it will be encoded as a `bytes` object based on the `encoding` parameter and constructed as an `Entity` object.


[](id:mime-type)
## Supported MIME Types

Dataway uses the `Entity` type to support various data types, including JSON, CSV, and XML. You can specify the MIME and encoding types in the value or raw data-based constructor to get an `Entity` object encapsulating different data types. You can use an `Entity` selector to read the parsed structure data.

Different MIME types have different data formats in `Entity`. The mappings are as listed below:

| MIME Type | Data Format |
| --------------------------------- | --------------------------------------- |
| application/json                  | [JSON format](#json-format)                   |
| application/x-www-form-urlencoded | [HTTP form format](#urlencode-format)          |
| text/plain                        | [Text format](#textplain-format)              |
| application/xml                   | [XML format](#xml-format)                     |
| application/csv                   | [CSV form format](#csv-format)                 |
| multipart/form-data               | [HTTP Form-Data form format](#formdata-format) |
| Other MIME types | [Other formats](#other-format) |

The encoding rules, data structures, and specific `Entity` selector syntax vary by data format. Different data formats are as detailed below:


[](id:json-format)
### JSON format

JSON data is the serialized data of an `Entity` object with the MIME type of `application/json`.
- If the [raw data-based constructor](#from-bytes) is used, Dataway will parse the input `str` or `bytes` object into a dictionary object.
- If the [value-based constructor](#from-value) is used, the input data can be of the list, dictionary, or multi-value dictionary type and will be parsed into a dictionary object.

Below are two examples of how to use JSON data:
<dx-tabs>
::: Example 1: Construct an `Entity` object in JSON format
This example shows how to construct an `Entity` object in JSON format by using an `Entity` constructor and use an `Entity` selector to get the attributes and data of the `Entity` object.
		
- **Input**
The Dataway runtime environment depends on component execution. Suppose a **Transform** component previous to a **Set Payload** component has set `payload` in the flow execution message `msg` and `msg.payload` is a dictionary object with the following internal structure:
```python
{
    "name": "zhangsan",
    "age": 10,
    "male": True,
    "brothers": ["lisi", "zhaowu"]
}
```

- **Dataway script**
The following Dataway script uses the value-based constructor to convert `msg.payload` of dictionary type into an `Entity` object, uses a selector to get the metadata and elements of the object, and returns the obtained content.
```python
def dw_process(msg):
    entity = Entity.from_value(msg.payload, mime_type='application/json', encoding='utf-8')
    return {
        'blob': entity['^blob'],
        'mimeType': entity['^mime_type'],
        'name': entity['name'],
        'brother': entity['brothers'][0],
        'male': entity['^value']['age'],
        'other': entity.get('other', 'other_default')
    }
```

- **Output**
The Dataway script output is a dictionary object:
```python
{
    "blob": b'{"name":"zhangsan","age":10,"male":true,"brothers":["lisi","zhaowu"]}',
    "mimeType": "application/json",
    "name": "zhangsan",
    "brother": "lisi",
    "male": 10,
    "other": "other_default"
}
```
:::
::: Example 2: Use a complex JSON structure
This example parses a complex JSON structure and runs in the **Set Payload** component.

- **Input**
The Dataway runtime environment depends on component execution. Suppose a **Transform** component previous to a **Set Payload** component has set `payload` in the flow execution message `msg` and `msg.payload` is an `Entity` object with the following internal structure:
```python
{
    'mime_type': 'application/json',
    'encoding': 'utf-8',
    'blob': b'{"name":"zhangsan","age":10,"male":true,"brothers":["lisi","zhaowu"]'
}
```

- **Dataway script**
The following Dataway script will process `msg` to get the target elements and return an `Entity` object:
```python
def dw_process(msg):
    val = {
        "k0": msg.payload['^blob'].decode(msg.payload['^encoding']),
        "k1": {
            "str": "str",
            "list": [123, "abc", 12.34],
            "dict": {
                "k1": "v1"
            }
        },
        "k2": math.sqrt(10),
        "k3": json.dumps({"a": 1, "b": [1, "d"]}),
        "k4": time.strftime('%Y-%m-%d %H:%M:%S'),
        "k5": "hello" + "world",
        "k6": ["12", 3] + [[1, 2], 4.5],
        "k8": msg.payload['^mime_type'],
    }
    if val['k8'] == 'application/json':
        val['k7'] = msg.payload.get('gbk')
        val['k9'] = time.time()
    return Entity.from_value(val, mime_type='application/json', encoding='utf-8')
```

- **Output**
The output result of the Dataway script is an `Entity` object. For the sake of clarity, the raw data in the `Entity` object is parsed and assigned to the `value` attribute:
```python
 {
    "mime_type": "application/json",
    "encoding": "utf-8",
    "value": {
        "k0": "{\"name\":\"zhangsan\",\"age\":10,\"male\":true,\"brothers\":[\"lisi\",\"zhaowu\"]}",
        "k1": {
            "str": "str",
            "list": [
                123,
                "abc",
                12.34
            ],
            "dict": {
                "k1": "v1"
            }
        },
        "k2": 3.1622776601683795,
        "k3": "{\"a\": 1, \"b\": [1, \"d\"]}",
        "k4": "2021-04-27 10:49:54",
        "k5": "helloworld",
        "k6": [
            "12",
            3,
            [
                1,
                2
            ],
            4.5
        ],
        "k8": "application/json",
        "k7": None,
        "k9": 1619491794.670995
    }
}
```
:::
</dx-tabs>



 [](id:urlencode-format)
### HTTP form format

HTTP form data is the parsed data of an `Entity` object with the MIME type of `application/x-www-form-urlencoded`.
- If the [raw data-based constructor](#from-bytes) is used, Dataway will parse the input string or `bytes` object into a dictionary object.
- If the [value-based constructor](#from-value) is used, the input data can be of the dictionary or multi-value dictionary type and will be parsed into a multi-value dictionary object.

**As its internal implementation is of the multi-value dictionary type, HTTP form data also supports special selector syntax in addition to general `Entity` selector syntax.**

| Selector | Description |
| -------- | --------------------------------- |
| ['*key'] | Returns all elements of `key` in the dictionary. |
| ['key']  | Returns the first element of `key` in the dictionary. |


#### Example: Construct and use an `Entity` object in HTTP form format
This example shows how to construct an `Entity` object in HTTP form format by using an `Entity` constructor and use `Entity` selector syntax to get the attributes and data of the `Entity` object.

- **Input**
`msg.payload` stores the HTTP form data `k1=123&k2=helloworld&k3=2&k3=abc`, which is represented as a multi-value dictionary object in Dataway and can be converted into a dictionary object. 
```python
{
    "k1": 123,
    "k2": "helloworld",
    "k3": [2, "abc"]
}
```

- **Dataway script**
The following Dataway script uses the value-based constructor to convert a dictionary object into an `Entity` object and uses a selector to get the metadata and elements of the object.
```python
def dw_process(msg):
    entity = Entity.from_value(msg.payload, mime_type='application/x-www-form-urlencoded', encoding='utf-8')
    return {
        'blob': entity['^blob'],
        'mimeType': entity['^mime_type'],
        'k1': entity['k1'],
        'k3': entity['^value']['k3'],
        'k3multi_selector': entity['^value']['*k3'],
        'k5': entity.get('k5', 'default_value')
    }
```

- **Output**
The Dataway script output is a dictionary object:
```python
{
    "blob": b'k1=123&k2=helloworld&k3=2&k3=abc',
    "mimeType": "application/x-www-form-urlencoded",
    "k1": 123,
    "k3": 2,
    "k3multi_selector": [2, "abc"],
    "k5": "default_value"
}
```


[](id:textplain-format)
### Text format

Text data is the parsed data of an `Entity` object with the MIME type of `text/plain`. In both the [value-based constructor](#from-value) and [raw data-based constructor](#from-bytes), the `data` parameter is a string or a `bytes` object, and the `Entity` object is a string.


#### Example: Construct an `Entity` object in text format
This example shows how to construct an `Entity` object in text format by using an `Entity` constructor and use `Entity` selector syntax to get the attributes and data of the `Entity` object.

- **Input**
`msg.payload` stores text data: "This is a text plain message".

- **Dataway script**
The following Dataway script uses the value-based constructor to convert a string into an `Entity` object and uses a selector to get the metadata and elements of the object.
```python
def dw_process(msg):
    entity = Entity.from_value(msg.payload, mime_type='text/plain', encoding='utf-8')
    return entity['^value']
```

- **Output**
The Dataway script output is a string: "This is a text plain message".


[](id:xml-format)
### XML format

XML data is the serialized data of an `Entity` object with the MIME type of `application/xml`.
- If the [raw data-based constructor](#from-bytes) is used, Dataway will parse the input string or `bytes` object into a dictionary object.
- If the [value-based constructor](#from-value) is used, the input data can be of only the dictionary type and will be parsed into a dictionary object. The input dictionary only contains a default key `root`, and the value is the built-in `MultiMap`, where you can manipulate the `msg` attributes as needed.

**XML data also supports special selector syntax in addition to general `Entity` selector syntax.**

| Selector | Description |
| --------- | ------------------------------------ |
| ['*key'] | Returns all elements of `key` on an XML node. |
| ['*key'] | Returns the first element of `key` on an XML node. |
| ['#text'] | Returns the text value of an XML node. |
| ['@attr'] | Returns the `attr` value of an XML node. |

Below are two examples of how to use XML data:

#### Example 1: Construct an `Entity` object in XML format

This example shows how to construct an `Entity` object in XML format by using an `Entity` constructor and use `Entity` selector syntax to get the attributes and data of the `Entity` object.

- **Input**
The value of `payload` in the Dataway input parameter `msg` is constant `1`, and `msg.vars` contains a key-value pair with the key of `abc` and the value of `123`.
```python
{
    "payload": 1,
    "vars": {
        "abc": "123"
    }
}
```

- **Dataway script**
The following Dataway script uses the [value-based method](#from-value) to convert a dictionary object into an `Entity` object and returns it:
```python
def dw_process(msg):
    a = math.floor(1.4)
    return Entity.from_value({
        'root': {
            'k1': msg.vars['abc'],
            'k2': json.dumps('Haha', ensure_ascii=False),
            'k3': a + 1,
            '@id': "hello",
            '#text': "<a>dwad</a>",
            'k4': ['abc', 'def', None],
        }
    }, mime_type = 'application/xml')
```

- **Output**
The output result of the Dataway script is an `Entity` object. Here, the raw data (`blob`) is a binary object in XML format:
```python
{
    "mime_type": "application/xml",
    "encoding": "utf-8",
    "blob": b'<?xml version="1.0" encoding="utf-8"?>
    <root id="hello"><k1>123</k1><k2>"Haha"</k2><k3>2</k3><k4>abc</k4><k4>def</k4><k4></k4><a>dwad</a></root>'
}
```

#### Example 2: Use a specific XML selector
This example shows how to use a selector of the specific syntax in XML data.

- **Input**
The value of `payload` in the Dataway input parameter `msg` is constant `1`, and `msg.vars` contains a key-value pair with the key of `abc` and the value of `123`.
```python
{
    "payload": 1,
    "vars": {
        "abc": "123"
    }
}
```

- **Dataway script**
The following Dataway script uses the [value-based constructor](#from-value) to convert a dictionary object into an `Entity` object and uses a selector to get the object data.
```python
def dw_process(msg):
    a = math.floor(1.4)
    entity =  Entity.from_value({
        'root': {
            'k1': msg.vars['abc'],
            'k2': json.dumps('Haha', ensure_ascii=False),
            'k3': a + 1,
            '@id': "hello",
            '#text': "<a>dwad</a>",
            'k4': ['abc', 'def', None],
        }
    }, mime_type = 'application/xml')
    return {
        'k1': entity['root']['#text'] + entity['root']['@id'],
        'k2': entity['root']['k1'],
        'k3': entity['root']['*k4']['^value'],
        'k4': entity['root']['k4'],
        'k5': entity['^mime_type']
    }
```

- **Output**
The Dataway script output is a dictionary object: 
  
```python
{
    "k1": "<a>dwad</a>hello",
    "k2": "123",
    "k3": ['abc', 'def', None],
    "k4": "abc",
    "k5": "application/xml"
}
```

>?In XML data, the `root` node is the default node, and its attributes are specified in the format of `@id=123` and text in the format of `#text`. The `root` value is of `MultiMap` type, where the key is the name of each child node and the value is the child node value.


<span id='csv-format'></span> 
### CSV format

CSV data is the serialized data of an `Entity` object with the MIME type of `application/csv`.
- If the [raw data-based constructor](#from-bytes) is used, Dataway will parse the input string or `bytes` object into a list data structure, where each element is a dictionary object.
- If the [value-based constructor](#from-value) is used, the input data can be of the list type and will be parsed into a list data structure, where each element is a dictionary object.


Below is an example of how to use CSV data:


#### Example: Construct an `Entity` object in CSV format
This example shows how to construct an `Entity` object in CSV format by using an `Entity` constructor and use `Entity` selector syntax to get the attributes and data of the `Entity` object.

- **Input**
The value of `payload` in the Dataway input parameter `msg` is constant `1`, and `msg.vars` contains a key-value pair with the key of `abc` and the value of `123`.
```python
{
    "payload": 1,
    "vars": {
        "abc": "123"
    }
}
```

- **Dataway script**
The following Dataway script uses the [value-based constructor](#from-value) to convert a dictionary object into an `Entity` object and uses selector syntax to get the object attribute values.
```python
def dw_process(msg):
    entity = Entity.from_value([
        {'k1':'abcd','k2':123.0,'k3':True},
        {'k1':'defs','k2':'dwdw,2e','k3':10},
    ], mime_type = 'application/csv')
    return {
        'var1': entity['^blob'],
        'var2': entity['^mime_type'],
        'var3': entity['^encoding'],
        'var4': entity[0]['k2'] + entity[1]['k3'],
        'var5': entity[1]['k2']
    }
```

- **Output**
The Dataway script output is a dictionary object:  
```python
{
    "var1": b'k1,k2,k3\r\nabcd,123.0,True\r\ndefs,"dwdw,2e",10\r\n',
    "var2": "application/csv",
    "var3": "utf-8",
    "var4": "133",
    "var5": "dwdw,2e"
}
```

>?For CSV data format, each element in the received list is a dictionary object. As the title line of the CSV text, the key in each element must be the same; the value of each element represents the value of the line, and multiple values are separated by comma.


[](id:formdata-format) 
### HTTP Form-Data form

HTTP Form-Data form data is the serialized data of an `Entity` object with the `mime-type` of `multipart/form-data`.

#### `multipart/form-data` in the browser

When a browser sends a request with the `Content-Type` of `multipart/form-data`, the actually transferred byte array is converted into a string as follows:

Each parameter starts with a boundary indicating the start of the parameter, such as `--34b21`. Note that `--` is the fixed start, and `34b21` is a random string of up to 70 characters generated by the browser.

The next two lines are the fixed headers of `Content-Disposition` and `Content-Type`. `Content-Disposition` contains two fields: `name` and `filename`. `Content-Type` is the `Content-Type` of the input content. `name` is the parameter name, and `filename` is the filename. If `filename` is `*.txt` or empty, `Content-Type` will be `text/plain` by default. If `filename` is another value, `Content-Type` will be set automatically based on the file extension. In addition, other extended headers are also supported.

The next line is the actual content. If `Content-Type` is `text/plain`, it will be a general string such as `Book`. If `Content-Type` is `application/json`, it will be a JSON string, such as the JSON structure of `file1`.

On the last line, `--34b21--` is used to mark the end of the request. 
```
--34b21
Content-Disposition: form-data; name="text"
Content-Type: text/plain

Book
--34b21
Content-Disposition: form-data; name="file1"; filename="a.json"
Content-Type: application/json

{
    "title": "Java 8 in Action",
    "author": "Mario Fusco",
    "year": 2014
}
--34b21
Content-Disposition: form-data; name="file2"; filename="a.html"
Content-Type: text/html

<!DOCTYPE html>
<title>
Available for download!
</title>
--34b21--
```


#### Form-Data construction and usage


- If the [raw data-based constructor](#from-bytes) is used, Dataway will parse the input string or `bytes` object into a [FormDataParts](#formdataparts) data structure.
- If the [value-based constructor](#from-value) is used, the input data can be of `Entity`, `Formdata`, list, or dictionary type and will be parsed into a [FormDataParts](#formdataparts) data structure.

>?
>- If an `Entity` object is input, the system first checks whether its MIME type is `multipart/form-data`, and if so, the `Entity` object will be directly returned; otherwise, an error will be reported.
>- If a `FormdataParts` object is input (the list/dictionary structure mentioned above), its value will be directly assigned to an `Entity` object.
>- If a list object is input, the data structure must be as follows: The first element is the parameter name; if the second element is a list, the first, second, third, and fourth items in the second element must be a filename, the actual content, `Content-Type`, and a dictionary (representing `extra_headers`) respectively. If the second element is a string, the filename is empty, the actual content is the string content, and `Content-Type` is `text/plain` by default.

**HTTP Form-Data data also supports special selector syntax in addition to general `Entity` selector syntax.**

| Selector | Description |
| --------------------------------------------------- | ----------------------------------------------- |
| ['parts'] | Returns data of the custom `FormDataParts` type.                 |
| <span>['parts']</span>[0]                           | Returns the zeroth item of `FormData`.                             |
| <span>['parts']</span><span>['a']</span>['content'] | Returns the `content` value in the value with the key of `a` in `FormDataParts`. |
| ['boundary']                                        | Returns the separator of `FormDataParts`.                       |

#### Examples
Below are two examples of how to use HTTP Form-Data:

<dx-tabs>
::: Example 1: Construct an `Entity` object in HTTP Form-Data format
This example shows how to construct an `Entity` object in HTTP Form-Data format by using an `Entity` constructor.

- **Input**
The variables (`vars`) in the Dataway input parameter `msg` contain a key-value pair with the key of `abc` and value of `123`.
```python
{
    "vars": {
        "abc": "123"
    }
}
```

- **Dataway script**
The following Dataway script uses the [value-based constructor](#from-value) to convert a dictionary object into an `Entity` object and returns it:
```python
def dw_process(msg):
    a = math.floor(1.4)
    c = Entity.from_value({
        'k1': msg.vars['abc'],
        'k2': json.dumps('Haha', ensure_ascii=False),
        'k3': a + 1,
    }, mime_type = 'application/json')
    return Entity.from_value(
        [
            ('a', ('test.json', '{"a": a}', 'application/json', {'Test111': 1})),
            ('b', '333'),
            ('c', ('c.json', c, c['^mime_type']))
        ],
        mime_type='multipart/form-data; boundary=123333333'
    )
```

- **Output**
The output result of the Dataway script is an `Entity` object. Here, the raw data (`blob`) is a binary object with the `multipart/form-data` structure:
```python
{
    "mime_type": "multipart/form-data; boundary=12345",
    "encoding": "utf-8",
    "blob": b'''--123333333
Content-Disposition: form-data; name="a"; filename="test.json"
Content-Type: application/json
Test111: 1

{"a": a}
--123333333
Content-Disposition: form-data; name="b"

333
--123333333
Content-Disposition: form-data; name="c"; filename="c.json"
Content-Type: application/json

{"k1":"123","k2":"\"Haha\"","k3":2}
--123333333--
'''
}
```
:::
::: Example 2: Use a Form-Data selector
This example shows how to use a selector of the specific syntax in Form-Data data.

- **Input**
`payload` in the Dataway input parameter `msg` is an `Entity` object, which is created through the [value-based constructor](#from-value). The object's MIME type is `multipart/form-data`.
```python
def dw_process(msg):
    return Entity.from_value(
        [('a', ('test', '1233', 'application/json', {'test111':1})),
        ('b', (None, '2333', 'text/plain')),],
        mime_type="multipart/form-data; boundary=ce560532019a77d83195f9e9873e16a1"
    )
```

- **Dataway script**
The following Dataway script will use a Form-Data selector to process `msg.payload` and return a dictionary object:
```python
def dw_process(msg):
    return {
        'k1': str(type(msg.payload)),
        'k2': msg.payload['^mime_type'],
        'k3': msg.payload['^encoding'],
        'k4': msg.payload['^blob'],
        'k5': msg.payload['boundary'],
        'k6': msg.payload['parts']['a']['headers']['Content-Disposition']['name']
						+ '-' + msg.payload['parts'][1]['headers']['Content-Type']
    }
```

- **Output**
The Dataway script output is a dictionary object:
```python
{
    'k1': 'Entity',
    'k2': 'multipart/form-data;boundary=ce560532019a77d83195f9e9873e16a1',
    'k3': 'utf-8',
    'k4': b'''--ce560532019a77d83195f9e9873e16a1
Content-Disposition: form-data; name="a"; filename="test"
Content-Type: application/json
test111: 1

1233
--ce560532019a77d83195f9e9873e16a1
Content-Disposition: form-data; name="b"
Content-Type: text/plain

2333
--ce560532019a77d83195f9e9873e16a1--
''',
		'k5': 'ce560532019a77d83195f9e9873e16a1',
		'k6': 'a-text/plain'
}
```

:::
</dx-tabs>



[](id:other-format)
### Other types

For data of other MIME types, Dataway cannot directly create it through the [value-based constructor](#from-value) but can read it from the upstream components or use the [raw data-based constructor](#from-bytes) to construct an encapsulated `Entity` object.

Suppose the input data is a binary `bytes` flow and a Dataway expression is used in the **Set Payload** component to encapsulates the `bytes` flow into `msg.payload`:
**Dataway expression**
```python
def dw_process(msg):
    b = msg.payload
    return Entity.from_bytes(b, mime_type='application/octet-stream')
```
You can use [`Entity` selector](#selectors) syntax for subsequent operations in downstream components.


[](id:dataref)
## Flow Data Panel

Dataway supports visual data reference. On the **Flow data** panel, you can click a data tag to reference the target data in the flow context, such as variable and previous component output. This lets you interconnect components more quickly and easily. Currently, all Dataway modes support visual data reference, including [text](https://www.tencentcloud.com/document/product/1165/51656), [expression](https://www.tencentcloud.com/document/product/1165/51657), [Python code](https://www.tencentcloud.com/document/product/1165/51659), and [Java code](https://www.tencentcloud.com/document/product/1165/51661) modes.

1. The **Flow data** panel will pop up automatically when you click the Dataway textbox.
2. On the **Flow data** panel, click a data tag to select it, and the Dataway textbox will directly reference the flow context data and insert the data tag where the cursor is.



Once a rule is created, you can write SQL statements to process the data in a certain type of topics. The IoT Hub console provides a simplified way to enter SQL statements.


For example, if you want to extract three fields `action`, `targetDevice`, and `count` from the JSON message in the `E23VBC3GE8/device_02/event` topic and then filter them by `count<=3` to get the final processed data for further forwarding, use the following rule:
![](https://main.qcloudimg.com/raw/b410d3b12e18d8b468ee4382a4993a31.png)

## Action
When you extract the desired fields from the topic, you should consider performing some operations on them, such as forwarding or storage. Currently supported operations include:
- Data forwarding to another topic
- Data forwarding to a third-party service
- Data forwarding to CKafka
- Data forwarding to a CMQ topic
- Data forwarding to a CMQ queue
- Data forwarding to CTSDB
- Data forwarding to TencentDB for MySQL
- Data forwarding to TencentDB for MongoDB

When triggering a forwarding action, the rule engine will encapsulate the payload reported by the device in JSON format as shown below:
1. JSON sample for forwarding to CMQ/CKafka:
```
{
  "MsgType":    "Publish",
  "Topic":      "AD4GVS5549/device/data",
  "Seq":        13107192,
  "PayloadLen": 17,
  "Payload":    "dGhpcyBpcyBhIGV4YW1wbGU=", 
  "ProductId":  "AD4GVS5549",
  "DeviceName": "device",
  "Time":       "2018-08-14 15:12:05",
}
```
 The descriptions of each field are as follows:
 - MsgType: valid values: Publish (forwarding to configured message queue), Forward (forwarding to the hit rule engine), StatusChange (status change).
 - PayloadLen: length of the payload of the message reported by the device in bytes.
 - Payload: payload of the original message, which will be Base64-encoded by default.
 - Event: it is present only for messages of the `StatusChange` type. Valid values: Online (connection), Offline (disconnection).
 - Time: the timestamp when the forwarding action is triggered.
2. JSON sample for forwarding to a third-party service (http forward):
```
{
	"devicename":"device",
    "payload":{
  	"params":{
       "power_switch":1,
       "color":1,
       "brightness":32
		}
	},
       "productid":"AD4GVS5549",
       "seq":2,
       "timestamp":1587109346,
       "topic":"AD4GVS5549/device/data"
}
```
 The descriptions of each field are as follows:
 - devicename: device name defined on the IoT Hub platform.
 - Payload: payload of the original message. If it is in JSON format, it will be passed through for forwarding; if it is in binary format, it will be Base64-encoded.
 - seq: internal auto-incrementing unique message identifier in `int` type.
 - timestamp: the Unix timestamp when the forwarding action is triggered.


## Notes
#### Field definition
 - A field can contain up to 300 asterisks, commas, dots, spaces, letters, and digits and cannot be empty.
 - A field indicates the key in JSON. If the data is in binary format, the field cannot be used for filtering, and `*` can be used to forward all binary data.
 - The reported JSON data can be in nested JSON format, such as {"device_status":{"switch":"on"}}, where `device_status.switch` can be used to get the value of `switch`.
 - SQL and JSON subarrays are not supported.



#### Topic wildcard definition
If you want to listen on multiple topics, you can use `#` and `+` wildcards to define them.
 - `#` represents 0 or more arbitrary topic segments, which can only be placed at the end of the topic.
 - `+` represents 1 arbitrary topic segment, which can be placed in the middle of the topic.

For example, `house_monitor/+/get`
- Can listen on topics such as `house_monitor/thermometer/get` and `house_monitor/door/get`.
- Cannot listen on the topic `house_monitor/door/switch/get`, because `+` can represent only 1 topic segment.

For example, `house_monitor/#`
- Can listen on topics such as `house_monitor/thermometer` and `house_monitor/door/switch/get`.
- Cannot listen on `house/#/get`, because `#` can only be placed at the end of the topic.

#### Condition definition
The [condition] expression is used to filter messages in the topic. Only when a message satisfies the [condition] expression will it be extracted for further processing. Supported expressions are listed in the table below:

| Operator | Description | Example |
|---|---|---|
|= | Equal to | color = 'red'|
|<> | Not equal to           | color <> 'red' |
|AND    | Logic AND           | color = 'red' AND siren = 'on'|
|OR | Logic OR           | color = 'red' OR siren = 'on'|
|( )    | The content in the parentheses is a complete entity  | color = 'red' AND (siren = 'on' OR siren ='isTest') |
|+  | Arithmetic addition          | age = 4 + 5 |
|-  | Arithmetic subtraction           | age = 5 - 4 |
|/  | Division             | age = 20 / 4 |
|*  | Multiplication             | age = 5 * 4 |
|%  | Remainder           | age = 0 % 6 |
|<  | Less than                | 5 < 6 |
|<= | Less than or equal to     | 5 <= 6|
|>  | Greater than                | 6 > 5|
|>= | Greater than or equal to     | 6 >= 5|

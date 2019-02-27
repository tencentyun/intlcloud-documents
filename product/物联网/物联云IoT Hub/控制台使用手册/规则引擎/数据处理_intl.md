[//]: # (chinagitpath:XXXXX)

Once the rule is created, you can write SQL to process the data from a certain topic type. The IoT Hub Console supports SQL writing to simplify SQL statements generation. The console filters topic data using the  conditions in the red box below.
![](https://main.qcloudimg.com/raw/4a9e8f0f4731648d1613e55380511266.png)

The rule expressed in the example below is:
Extract the ```action targetDevice count``` field of the JSON message in the ```E23VBC3GE8/device_02/event``` topic and filter the data by ```count <=3``` to get the final processed data for further data forwarding.
![](https://main.qcloudimg.com/raw/bdeab8841c4f62434bb925fecfd27a00.png)

## Topic Actions
When you extract the desired fields from the topic, you should consider performing some operations on them, such as forwarding or storage. Currently supported operations include:
- Data forwarding to another topic
- Data forwarding to third-party services
- Data forwarding to CKafka
- Data forwarding to CMQ topic
- Data forwarding to CTSDB
- Data forwarding to TencentDB for MySQL
- Data forwarding to TencentDB for MongoDB

## For Reference

### Detailed Topic Wildcard Definition

If you want to monitor multiple topics, you can use the ```#``` and ```+``` wildcards to define them.
 - ```#``` represents 0 or more arbitrary topic segments, which can only be placed at the end of the topic.
 - ```+``` represents 1 arbitrary topic segment, which can be placed in the middle of the topic.

For example:, ```house_monitor/+/get```
can monitor topics such as ```house_monitor/thermometer/get``` and ```house_monitor/door/get```;
however, it cannot monitor the topic ```house_monitor/door/switch/get```, because ```+``` can only represent 1 topic segment.

For example, ```house_monitor/#```
can monitor topics such as ```house_monitor/thermometer``` and ```house_monitor/door/switch/get```;
however, ```house/#/get``` is invalid, because ```#``` can only be placed at the end of the topic.

### Detailed Condition Definition
The [condition] expression is used to filter the messages in the topic. Only when a message satisfies the [condition] expression will it be extracted for further processing. The table below lists the supported expressions:

| Operator | Description | Example |
|---|---|---|
|= | Equal to | color = 'red'|
| <> | Not equal to | color <> 'red' |
| AND | Logic and | color = 'red' AND siren = 'on' |
| OR | Logic or | color = 'red' OR siren = 'on' |
| ( ) | The content in the parentheses is a complete entity | color = 'red' AND (siren = 'on' OR isTest) |
|+ | Arithmetic addition | 4 + 5 |
| - | Arithmetic subtraction | 5 - 4 |
| / | Division | 20 / 4 |
|* | Multiplication | 5 * 4 |
| % | Remainder | 20 % 6 |
| < | Less than | 5 < 6 |
| <= | Less than or equal to | 5 <= 6 |
| > | Greater than | 6 > 5 |
| >= | Greater than or equal to | 6 >= 5 |
| CASE … WHEN … THEN … ELSE …END | Case expression | CASE col WHEN 1 THEN 'Y' WHEN 0 THEN 'N' ELSE '' END as flag|
| IN | Only enumeration is supported; sub-query is not supported. | For example, where a in(1,2,3); the following form is not supported: where a in(select xxx) |


### Device Connection

<table>
<thead>
<tr>
<th colspan="2">
Type and Description	
</th>
<th>
Limit
</th>
<tr>
</thead>
<tr>
<td>
Products
</td>
<td>
Maximum number of products that can be created under a single account
</td>
<td>
2,000
</td>
</tr>
<tr>
<td>
Devices
</td>
<td>
Maximum number of devices that can be added under a single product
</td>
<td>
1,000,000
</td>
</tr>
<tr>
<td>
Gateways and subdevices
</td>
<td>
Maximum number of subdevices that can be added under a single gateway
</td>
<td>
1500
</td>
</tr>
<tr>
<td  rowspan="3">
Device groups
</td>
<td>
Maximum number of parent groups and subgroups in total allowed for a single account
</td>
<td>
Unlimited
</td>
<tr>
<td>
Maximum number of devices that can be added to a single group
</td>
<td>
Unlimited
</td>
</tr>
<tr>
<td>
Maximum number of groups that a single device can be added to
</td>
<td>
Unlimited
</td>
</tr>
<tr>
<td>
Remote configuration
</td>
<td>
Maximum size of remote the configuration file. Supports JSON format only.
</td>
<td>
8 KB
</td>
</tr>
<tr>
</thead>
<tr>
<td>
Data storage time
</td>
<td>
Storage time in days of the attribute, event, service data generated when the product is running.
</td>
<td>
7
</td>
</tr>
<tr>
<td rowspan="2">
File management
</td>
<td>
Maximum size of all files that can be stored in the IoT Hub server for a single account.
</td>
<td>
1 GB
</td>
</tr>
<tr>
<td>
Maximum number of files that can be stored for a single device.
</td>
<td>
1,000
</td>
</tr>
<tr>
<td rowspan="2">
OTA update
</td>
<td>
Maximum size of a single update package file allowed
</td>
<td>
1,024 MB
</td>
</tr>
<tr>
<td>
Maximum number of devices that can be updated in a single batch update
</td>
<td>
10,000
</td>
</tr>
</table>

### Message Communication

<table>
<thead>
<tr>
<th colspan="2">
Type and Description	
</th>
<th>
Limit
</th>
<tr>
</thead>
<tr>
<td>
Device connection restriction
</td>
<td>
With the same device certificate information, only one connection can be established with the platform server concurrently.
</td>
<td>
Yes
</td>
</tr>
<tr>
<td>
Connection requests
</td>
<td>
Maximum number of MQTT connection requests per second allowed for a single device
</td>
<td>
1 request/5s
</td>
</tr>
<tr>
<td>
Device subscriptions
</td>
<td>
Maximum number of subscriptions allowed for a single device
</td>
<td>
Unlimited
</td>
</tr>
<tr>
<td  rowspan="2">
Requests
</td>
<td>
Number of requests sent from the device side to the IoT Hub platform per second allowed for a single account
</td>
<td>
Unlimited
</td>
<tr>
<td>
Number of requests sent from the IoT Hub platform to the device side per second allowed for a single account
</td>
<td>
Unlimited
</td>
</tr>
<tr>
<td rowspan="2">
Message communication traffic restriction
</td>
<td>
Maximum number of messages that a single device can report per second
</td>
<td>
30
</td>
</tr>
<tr>
<td>
Maximum number of messages that a single device can receive per second (subject to the network environment)
</td>
<td>
50
</td>
</tr>
<tr>
<td>
Bandwidth
</td>
<td>
Maximum throughput (bandwidth) per second allowed for a single connection
</td>
<td>
Unlimited
</td>
</tr>
<tr>
<td>
Cache requests
</td>
<td>
Maximum number of unconfirmed inbound publish requests allowed per client
</td>
<td>
150
</td>
</tr>
<tr>
<td>
Message storage duration
</td>
<td>
Maximum storage time of QoS1 messages
</td>
<td>
24h
</td>
</tr>
<tr>
<td>
MQTT message size 
</td>
<td>
Maximum size allowed for a single published MQTT message. If this limit is exceeded, the publish request will be rejected.
</td>
<td>
16 KB
</td>
</tr>
<tr>
<td>
CoAP message size
</td>
<td>
Maximum size allowed for a single published CoAP message. If this limit is exceeded, the publish request will be rejected.
</td>
<td>
1 KB
</td>
</tr>
<tr>
<td>
MQTT keepalive
</td>
<td>
MQTT connection heartbeat time. If the heartbeat time is not within this limit, the server will reject the connection request. </td>
<td>
900s
</td>
</tr>
<tr>
<td>
RRPC timeout period
</td>
<td>
Timeout period of device response to RRPC request
<td>
10s
</td>
</tr>
<tr>
<td rowspan="2">
Offline message
</td>
<td>
Number of offline messages
<td>
Up to 150 messages per device
</td>
</tr>
<tr>
<td>
Storage period of offline messages
<td>
Messages can be stored for up to 24 hours.
</td>
</tr>
<tr>
<td>
`KeepAlive` value
</td>
<td>
Value range of `KeepAlive`
<td>
0-900s
</td>
</tr>
</table>

### Topic

<table>
<thead>
<tr>
<th colspan="2">
Type and Description	
</th>
<th>
Limit
</th>
<tr>
</thead>
<tr>
<td>
Custom topic classes
</td>
<td>
Maximum number of custom topic classes allowed for a single product</td>
<td>
100
</td>
</tr>
<tr>
<td>
Topic length
</td>
<td>
Maximum length of a topic allowed
</td>
<td>
255 UTF-8 encoded characters
</td>
</tr>
<tr>
<td>
Topic levels
</td>
<td>
Maximum number of hierarchical levels that can be contained in a topic, that is, maximum number of slashes in a topic</td>
<td>
10
</td>
</tr>
<tr>
<td>
Subscriptions
</td>
<td>
Maximum number of subscriptions allowed per subscribe request
</td>
<td>
1
</td>
</tr>
<tr>
<td>
Operation effective time
</td>
<td>
Effective time of a subscription or unsubscription operation
</td>
<td>
5s
</td>
</tr>
<tr>
<td rowspan="2">
Broadcast topic
</td>
<td>
Restrictions on the body of the message to broadcast
</td>
<td>
Max 8 KB. the original message must be converted into binary data and encoded with Base64 to generate the message body.
</td>
</tr>
<tr>
<td>
Message broadcasts by the server side to all devices per minute 
</td>
<td>
A single product can perform only one task at a time.
</td>
</tr>
</table>

### Rule Engine

<table>
<thead>
<tr>
<th colspan="2">
Type and Description	
</th>
<th>
Limit
</th>
<tr>
</thead>
<tr>
<td>
Rules
</td>
<td>
Maximum number of rules that can be set for a single account
</td>
<td>
100
</td>
</tr>
<tr>
<td>
Data forwarding destinations
</td>
<td>
Maximum number of data forwarding actions allowed in a rule
</td>
<td>
10
</td>
</tr>
<tr>
<td>
Messages processed by rule engine
</td>
<td>
The data processing capability of an account
</td>
<td>
None
</td>
</tr>
<tr>
<td>
Written message count
</td>
<td>
The data forwarding capability of an account when the performance of the target cloud product instance is sufficient.
</td>
<td>
None
</td>
</tr>
<tr>
<td>
Requirements of data forwarding destinations
</td>
<td>
Data forwarding depends on the target product. Make sure that the instance of the target cloud product runs properly. Message forwarding fails in multiple scenarios. These scenarios include instance failure, overdue payments, parameter error, and configuration error.
</td>
<td>
The instance must run properly.
</td>
</tr>
<tr>
<td>
Message deduplication
</td>
<td>
When you forward a message, the message may be repeatedly sent until the client returns ACK or the message expires.
</td>
<td>
None. Each message has a unique ID.
</td>
</tr>
</table>

### Device Shadow and Server-Side Subscription 

<table>
<thead>
<tr>
<th colspan="2">
Type and Description	
</th>
<th>
Limit
</th>
<tr>
</thead>
<tr>
<td>
JSON Levels
</td>
<td>
Maximum number of levels that can be specified in a device shadow JSON file
</td>
<td>
5
</td>
</tr>
<tr>
<td>
File size
</td>
<td>
Maximum size of a device shadow JSON file
</td>
<td>
8 KB
</td>
</tr>
<tr>
<td>
Attributes
</td>
<td>
Maximum number of attributes that can be specified in a device shadow JSON file
</td>
<td>
None
</td>
</tr>
<tr>
<td>
Requests per second
</td>
<td>
Maximum number of requests per second per device</td>
<td>
None
</td>
</tr>
<tr>
<td>
Retry policy upon push failure
</td>
<td>
Due to the consumer client being disconnected and the slow consumption of messages, messages cannot be consumed in real time and instead enter the stacked queue. </td>
<td>
None
</td>
</tr>
</table>

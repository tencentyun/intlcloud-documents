## Attribute

Device attributes

Referenced by: CreateDevice.

| Name | Type | Required | Description |
|------|------|----------|------|
| Tags | Array of [DeviceTag](#DeviceTag) | No | List of attributes |

## BatchPublishMessage

Batch message publishing request

Referenced by: CreateTask.

| Name | Type | Required | Description |
|------|------|----------|------|
| Topic | String | Yes | The topic to which the message is published. It is the part after removing the ProductID and DeviceName from the Topic permission, such as "event" |
| Payload | String | Yes | Message content |

## BatchUpdateShadow

Batch device shadow updating task

Referenced by: CreateTask.

| Name | Type | Required | Description |
|------|------|----------|------|
| Desired | String | Yes | The desired state of the device shadow in the format of a string after JSON object serialization |

## DeviceInfo

Device details

Referenced by: DescribeDevices.

| Name | Type | Description |
|------|------|-------|
| DeviceName | String | Device name |
| Online | Integer | Whether the device online; 0 - offline; 1 - online |
| LoginTime | Integer | Login time of the device |
| Version | String | Device version |
| DeviceCert | String | Device certificate; returned for devices encrypted with certificates |
| DevicePsk | String | Device key; returned for devices encrypted with keys |
| Tags | Array of [DeviceTag](#DeviceTag) | Device attributes |
| DeviceType | Integer | Device type |
| Imei | String | IMEI |
| Isp | Integer | ISP type |
| NbiotDeviceID | String | DeviceID at the NB IoT ISP |
| ConnIP | Integer | IP address |
| LastUpdateTime | Integer | Last update time of the device |
| LoraDevEui | String | DevEui of a LoRa device |
| LoraMoteType | Integer | MoteType of a LoRa device |

## DeviceTag

Device attributes

Referenced by: CreateDevice, DescribeDevice, DescribeDevices.

| Name | Type | Required | Description |
|------|------|----------|------|
| Tag | String | Yes | Attribute name |
| Type | Integer | Yes | Type of attribute value; 1 - int, 2 - string |
| Value | String | Yes | Attribute value |

## Filter

Used to describe key-value pair filters for conditional filtering queries, such as filtering ID, name and state.

Referenced by: DescribeProducts.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | Name of the filter key |
| Values | Array of String | Yes | One or more filter values |

## MultiDevicesInfo

Device information returned when the device is created

Referenced by: DescribeMultiDevices.

| Name | Type | Description |
|------|------|-------|
| DeviceName | String | Device name |
| DevicePsk | String | Symmetric encryption key encoded with Base64; this parameter will be returned if symmetric encryption is used |
| DeviceCert | String | Device certificate; this parameter will be returned if asymmetric encryption is used |
| DevicePrivateKey | String | Private key of the device; this parameter will be returned if asymmetric encryption is used. Tencent Cloud caches it for the user, and its lifecycle is the same as that of the task.
| Result | Integer | Error code |
| ErrMsg | String | Error message |

## ProductInfo

Product details

Referenced by: DescribeProducts.

| Name | Type | Description |
|------|------|-------|
| ProductId | String | Product ID |
| ProductName | String | Product name |
| ProductMetadata | [ProductMetadata](#ProductMetadata) | Product metadata |
| ProductProperties | [ProductProperties](#ProductProperties) | Product attributes |

## ProductMetadata

Product metadata

Referenced by: DescribeProducts.

| Name | Type | Description |
|------|------|-------|
| CreationDate | Integer | Product creation time |

## ProductProperties

Product attributes

Referenced by: CreateProduct, DescribeProducts.

| Name | Type | Required | Description |
|------|------|----------|------|
| ProductDescription | String | No | Product description |
| EncryptionType | String | No | Encryption type; 1 - asymmetric encryption, 2 - symmetric encryption. If not entered, 1 is used by default |
| Region | String | No | Product region; currently only Guangzhou (gz) is supported |
| ProductType | Integer | No | Product type; 0 - normal device, 2 - NB-IoT device; 0 by default |
| Format | String | No | Data format; value: json or custom; json by default |
| Platform | String | No | Platform of the product; 0 by default |
| Appeui | String | No | AppEUI at the LoRa product operation side; only required for LoRa products |
| ModelId | String | No | ID of the thing model bound with the product; -1 - no binding |
| ModelName | String | No | Name of the thing model bound with the product |

## Task

Task description details

Referenced by: CreateTask.

| Name | Type | Required | Description |
|------|------|----------|------|
| UpdateShadowTask | [BatchUpdateShadow](#BatchUpdateShadow) | No | Description details of the batch shadow updating task; if the value of taskType is "UpdateShadow", this field is required. See BatchUpdateShadow below |
| PublishMessageTask | [BatchPublishMessage](#BatchPublishMessage) | No | Description details of the batch message publishing task; if the value of taskType is "PublishMessage", this field is required. See BatchPublishMessage below |

## TaskInfo

Task list details

Referenced by: DescribeTasks.

| Name | Type | Description |
|------|------|-------|
| Type | String | Task type; value: "UpdateShadow" or "PublishMessage" |
| Id | String | Task ID |
| ProductId | String | Product ID |
| Status | Integer | Status. 1 - waiting for processing, 2 - scheduling, 3 - completed, 4 - failed, 5 - canceled |
| CreateTime | Integer | Task creation time; a Unix timestamp |
| UpdateTime | Integer | Last update time of the task; a Unix timestamp |
| RetCode | Integer | Error code returned |
| ErrMsg | String | Error messages returned |

## TopicRulePayload

Packet of the rule creation request

Referenced by: CreateTopicRule, ReplaceTopicRule.

| Name | Type | Required | Description |
|------|------|----------|------|
| Sql | String | No | SQL statement of the rule encoded with Base64 |
| Actions | String | No | JSON string of the action; below is an example for most types: <br/>[{"republish":{"topic":"TEST/test"}},{"forward":{"api":"http://127.0.0.1:8080"}},{"ckafka":{"instance":{"id":"ckafka-test","name":""},"topic":{"id":"topic-test","name":"test"},"region":"gz"}},{"cmqqueue":{"queuename":"queue-test-TEST","region":"gz"}},{"mysql":{"instanceid":"cdb-test","region":"gz","username":"test","userpwd":"*****","dbname":"d_mqtt","tablename":"t_test","fieldpairs":[{"field":"test","value":"test"}],"devicetype":"CUSTOM"}}] |
| Description | String | No | Rule description |
| RuleDisabled | Boolean | No | The rule does not take effect |


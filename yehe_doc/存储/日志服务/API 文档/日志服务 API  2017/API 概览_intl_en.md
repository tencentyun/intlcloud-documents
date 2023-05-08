>! 
> - CLS APIs in this document are legacy and not updated any more. They are not supported by new CLS features, so we strongly recommend you use [CLS API 3.0](https://intl.cloud.tencent.com/document/product/614/42757).
> - To create log topics or modify index configurations, use [CLS API 3.0](https://intl.cloud.tencent.com/document/product/614/42757). To collect logs, use the [SDK](https://intl.cloud.tencent.com/document/product/614/45006) specially optimized for log collection.

## API upgrade guide
Commonly used legacy APIs can be upgraded to CLS API 3.0 as instructed below:

| Legacy: CLS API 2017 | API Documentation                                                  | New: CLS API 3.0       | API Documentation                                                  |
| --------------------- | ------------------------------------------------------------ | ------------------------- | ------------------------------------------------------------ |
| /topic                | [Getting Log Topic Information](https://intl.cloud.tencent.com/document/product/614/16887)<br />[Modifying Log Topic](https://intl.cloud.tencent.com/document/product/614/16884) | DescribeTopicsModifyTopic | [DescribeTopics](https://intl.cloud.tencent.com/document/product/614/42783)<br />[ModifyTopic](https://intl.cloud.tencent.com/document/product/614/42782) |
| /searchlog            | [Searching for Log](https://intl.cloud.tencent.com/document/product/614/16875) | SearchLog                 | [SearchLog](https://intl.cloud.tencent.com/document/product/614/42788) |
| /index                | [Getting Index Information](https://intl.cloud.tencent.com/document/product/614/16906)<br />[Modifying Index Information](https://intl.cloud.tencent.com/document/product/614/16905) | DescribeIndexModifyIndex  | [DescribeIndex](https://intl.cloud.tencent.com/document/product/614/42803)<br />[ModifyIndex](https://intl.cloud.tencent.com/document/product/614/42802) |
| /shipper              | [Getting Shipping Configuration](https://intl.cloud.tencent.com/document/product/614/16894) | DescribeShipperTasks      | [DescribeShipperTasks](https://intl.cloud.tencent.com/document/product/614/42773) |
| /pulllogs             | [Consumption Data](https://intl.cloud.tencent.com/document/product/614/34651) | OpenKafkaConsumer         | [OpenKafkaConsumer](https://intl.cloud.tencent.com/document/product/614/46784) |
| /consumergroups       | [Getting Consumer Group List](https://intl.cloud.tencent.com/document/product/614/34653) | OpenKafkaConsumer         | [OpenKafkaConsumer](https://intl.cloud.tencent.com/document/product/614/46784) |
| /consumerheartbeat    | [Consumer Heartbeat](https://intl.cloud.tencent.com/document/product/614/34652) | OpenKafkaConsumer         | [OpenKafkaConsumer](https://intl.cloud.tencent.com/document/product/614/46784) |
| /cursor               | [Getting Consumption Cursor](https://intl.cloud.tencent.com/document/product/614/34649) | OpenKafkaConsumer         | [OpenKafkaConsumer](https://intl.cloud.tencent.com/document/product/614/46784) |
| /consumergroupcursor  | [Getting Consumer Group Cursor](https://intl.cloud.tencent.com/document/product/614/34650)<br />[Modifying Consumer Group Cursor](https://intl.cloud.tencent.com/document/product/614/34655) | OpenKafkaConsumer         | [OpenKafkaConsumer](https://intl.cloud.tencent.com/document/product/614/46784) |

>?Here, `/pulllogs`, `/consumergroups`, `/consumerheartbeat`, `/cursor`, and `/consumergroupcursor` are CLS data consumption APIs. The feature has been upgraded to consumption over Kafka feature that is more compliant with open-source standards. You can perform an overall upgrade as instructed in [Consumption over Kafka](https://intl.cloud.tencent.com/document/product/614/42752).



## Log management

| API | Description |
| ------------------------------------------------------------ | ---------------------------------- |
| [Uploading a structured log](https://intl.cloud.tencent.com/document/product/614/50267) | Uploads a log to a specified log topic           |
| [Getting a log cursor](https://www.tencentcloud.com/document/product/614/16876) | Gets and downloads a log cursor under a specified log topic |
| [Searching for a log](https://intl.cloud.tencent.com/document/product/614/16875) | Searches for a log by the specified condition |
| [Downloading a log](https://intl.cloud.tencent.com/document/product/614/16874) | Downloads a log with the cursor |

## Logset management

| API | Description |
| ------------------------------------------------------------ | --------------------------- |
| [Create a Logset](https://intl.cloud.tencent.com/document/product/614/16879) | Creates a logset. ID of the new logset is returned. |
| [Get Logset Information](https://intl.cloud.tencent.com/document/product/614/16881) | Gets the information of a logset |
| [Get Logset List](https://intl.cloud.tencent.com/document/product/614/16882) | Gets the list of logset information |
| [Modify a Logset](https://intl.cloud.tencent.com/document/product/614/16878) | Modifies a logset |
| [Delete a Logset](https://intl.cloud.tencent.com/document/product/614/16880) | Deletes a logset |

## Log topic management

| API | Description |
| ------------------------------------------------------------ | ------------------------------- |
| [Create a Log Topic](https://intl.cloud.tencent.com/document/product/614/16885) | Creates a log topic. ID of the new log topic is returned. |
| [Get Log Topic Information](https://intl.cloud.tencent.com/document/product/614/16887) | Gets the information of a log topic |
| [Get the Server Groups Bound to a Log Topic](https://intl.cloud.tencent.com/document/product/614/30433) | Gets the information of the server group bound to a log topic |
| [Get Log Topic List](https://intl.cloud.tencent.com/document/product/614/16888) | Gets the list of log topic information |
| [Modify a Log Topic](https://intl.cloud.tencent.com/document/product/614/16884) | Modifies a log topic |
| [Configure the Server Groups Bound to a Log Topic](https://intl.cloud.tencent.com/document/product/614/30434) | Sets the information of the server group bound to a log topic |
| [Delete a Log Topic](https://intl.cloud.tencent.com/document/product/614/16886) | Deletes a log topic |
| [Getting the list of topic partitions](https://intl.cloud.tencent.com/document/product/614/34659) |     Gets the list of topic partitions             |
| [Merging a topic partition](https://intl.cloud.tencent.com/document/product/614/34660) | Merges a topic partition in read/write state                 |
| [Splitting a topic partition](https://intl.cloud.tencent.com/document/product/614/34661) | Splits a topic partition in read/write state                  |




## Shipping task management

| API | Description |
| ------------------------------------------------------------ | -------------------------- |
| [Create a Shipping Task](https://intl.cloud.tencent.com/document/product/614/16890) | Creates a shipping task |
| [Get Shipping Configuration](https://intl.cloud.tencent.com/document/product/614/16894) | Gets the details of a specified shipping policy |
| [Get Log Topic Shipping List](https://intl.cloud.tencent.com/document/product/614/30435) | Gets the details of the shipping policy under a specified log topic |
| [Get Shipping Task List](https://intl.cloud.tencent.com/document/product/614/16891) | Gets the list of shipping task information |
| [Modify a Shipping Task](https://intl.cloud.tencent.com/document/product/614/16893) | Modifies an existing shipping task |
| [Retry a Failed Task](https://intl.cloud.tencent.com/document/product/614/16895) | Retries a failed shipping task |
| [Delete Shipping Configuration](https://intl.cloud.tencent.com/document/product/614/16892) | Deletes shipping configuration |

## Machine group management

| API | Description |
| ------------------------------------------------------------ | --------------------------- |
| [Create a Server Group](https://intl.cloud.tencent.com/document/product/614/16899) | Creates a server group. ID of the new server group is returned. |
| [Get Server Group Information](https://intl.cloud.tencent.com/document/product/614/16902) | Gets the information of a server group |
| [Get Server Status](https://intl.cloud.tencent.com/document/product/614/16901) | Gets the status of a server under the specified server group |
| [Get Server Group List](https://intl.cloud.tencent.com/document/product/614/16903) | Gets the list of server group information |
| [Modify a Server Group](https://intl.cloud.tencent.com/document/product/614/16898) | Modifies a server group |
| [Delete a Server Group](https://intl.cloud.tencent.com/document/product/614/16900) | Deletes a server group |


## Consumption management

| API | Description |
| ------------------------------------------------------------ | --------------------------- |
|[Creating a consumer group](https://intl.cloud.tencent.com/document/product/614/34648) | Creates a consumer group |
| [Getting the consumption cursor](https://intl.cloud.tencent.com/document/product/614/34649) | Gets the consumption cursor |
| [Getting the consumer group cursor](https://intl.cloud.tencent.com/document/product/614/34650) | Gets the consumer group cursor |
| [Consuming data](https://intl.cloud.tencent.com/document/product/614/34651) | Consumes a log |
| [Uploading consumer heartbeats](https://intl.cloud.tencent.com/document/product/614/34652) | Uploads consumer heartbeats |
| [Getting the list of consumer groups](https://intl.cloud.tencent.com/document/product/614/34653) | Gets the list of consumer groups of a log topic |
| [Modifying a consumer group](https://intl.cloud.tencent.com/document/product/614/34654) | Modifies a consumer group |
| [Modifying the consumer group cursor](https://intl.cloud.tencent.com/document/product/614/34655) | Modifies the consumer group cursor |
| [Deleting a consumer group](https://intl.cloud.tencent.com/document/product/614/34656) | Deletes a consumer group |






## Index management

| API | Description |
| ------------------------------------------------------------ | -------------------------- |
| [Get Index Information](https://intl.cloud.tencent.com/document/product/614/16906) | Gets the details of a specified index policy |
| [Modify an Index Task](https://intl.cloud.tencent.com/document/product/614/16905) | Modifies an existing index task |

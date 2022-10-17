>! 
> - CLS APIs in this document are legacy and not updated any more. They are not supported by new CLS features, so we strongly recommend you use [CLS API 3.0](https://intl.cloud.tencent.com/document/product/614/42757).
> - To create log topics or modify index configurations, use [CLS API 3.0](https://intl.cloud.tencent.com/document/product/614/42757). To collect logs, use the [SDK](https://www.tencentcloud.com/document/product/614/45006) specially optimized for log collection.
> 

## Log management

| API | Description |
| ------------------------------------------------------------ | ---------------------------------- |
| [Uploading a structured log](https://www.tencentcloud.com/document/product/614/16873) | Uploads a log to a specified log topic |
| [Getting a log cursor](https://www.tencentcloud.com/document/product/614/16876) | Gets and downloads a log cursor under a specified log topic |
| [Searching for a log](https://intl.cloud.tencent.com/document/product/614/16875) | Searches for a log by the specified condition |
| [Downloading a log](https://intl.cloud.tencent.com/document/product/614/16874) | Downloads a log with the cursor |

## Logset management

| API | Description |
| ------------------------------------------------------------ | --------------------------- |
| [Creating a logset](https://intl.cloud.tencent.com/document/product/614/16879) | Creates a logset and returns the new logset ID |
| [Getting the logset information](https://intl.cloud.tencent.com/document/product/614/16881) | Gets the logset information |
| [Getting the list of logsets](https://intl.cloud.tencent.com/document/product/614/16882) | Gets the list of logsets |
| [Modifying a logset](https://intl.cloud.tencent.com/document/product/614/16878) | Modifies a logset |
| [Deleting a logset](https://intl.cloud.tencent.com/document/product/614/16880) | Deletes a logset |

## Log topic management

| API | Description |
| ------------------------------------------------------------ | ------------------------------- |
| [Creating a log topic](https://intl.cloud.tencent.com/document/product/614/16885) | Creates a log topic and returns the new log topic ID |
| [Getting the log topic information](https://intl.cloud.tencent.com/document/product/614/16887) | Gets the log topic information |
| [Getting the machine group bound to a log topic](https://intl.cloud.tencent.com/document/product/614/30433) | Gets the information of the machine group bound to a log topic |
| [Getting the list of log topics](https://intl.cloud.tencent.com/document/product/614/16888) | Gets the list of log topics |
| [Modifying a log topic](https://intl.cloud.tencent.com/document/product/614/16884) | Modifies a log topic |
| [Setting the machine group bound to a log topic](https://intl.cloud.tencent.com/document/product/614/30434) | Sets the machine group bound to a log topic |
| [Deleting a log topic](https://intl.cloud.tencent.com/document/product/614/16886) | Deletes a log topic |
| [Getting the list of topic partitions](https://intl.cloud.tencent.com/document/product/614/34659) |     Gets the list of topic partitions              |
| [Merging a topic partition](https://intl.cloud.tencent.com/document/product/614/34660) | Merges a topic partition in read/write state                 |
| [Splitting a topic partition](https://intl.cloud.tencent.com/document/product/614/34661) | Splits a topic partition in read/write state                  |




## Shipping task management

| API | Description |
| ------------------------------------------------------------ | -------------------------- |
| [Creating a shipping task](https://intl.cloud.tencent.com/document/product/614/16890) | Creates a shipping task |
| [Getting the shipping configuration](https://intl.cloud.tencent.com/document/product/614/16894) | Gets the details of the specified shipping policy |
| [Getting the list of log topic shipping policies](https://intl.cloud.tencent.com/document/product/614/30435) | Gets the detailed list of shipping policies under the specified log topic |
| [Getting the list of shipping tasks](https://intl.cloud.tencent.com/document/product/614/16891) | Gets the list of shipping tasks |
| [Modifying a shipping task](https://intl.cloud.tencent.com/document/product/614/16893) | Modifies an existing shipping task |
| [Retrying a failed task](https://intl.cloud.tencent.com/document/product/614/16895) | Retries a failed shipping task |
| [Deleting the shipping configuration](https://intl.cloud.tencent.com/document/product/614/16892) | Deletes the shipping configuration |

## Machine group management

| API | Description |
| ------------------------------------------------------------ | --------------------------- |
| [Creating a machine group](https://intl.cloud.tencent.com/document/product/614/16899) | Creates a machine group and returns the new machine group ID |
| [Getting the machine group information](https://intl.cloud.tencent.com/document/product/614/16902) | Gets the machine group information |
| [Getting the machine status](https://intl.cloud.tencent.com/document/product/614/16901) | Gets the status of a machine under the specified machine group |
| [Getting the list of machine group](https://intl.cloud.tencent.com/document/product/614/16903) | Gets the list of machine groups |
| [Modifying a machine group](https://intl.cloud.tencent.com/document/product/614/16898) | Modifies a machine group |
| [Deleting a machine group](https://intl.cloud.tencent.com/document/product/614/16900) | Deletes a machine group |


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
| [Getting the index information](https://intl.cloud.tencent.com/document/product/614/16906) | Gets the details of the specified index policy |
| [Modifying an index task](https://intl.cloud.tencent.com/document/product/614/16905) | Modifies an existing index task |

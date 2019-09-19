## 1. API Description
API domain name: `ckafka.api.qcloud.com`
This API (GetGroupOffsets) is used to get the CKafka consumer group offset under the user account.

## 2. Input Parameters
The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/431/5883).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
|instanceId | Yes | String| (Filter) Filter by instance ID |
|group| Yes |String | CKafka consumer group |
|topics| No |String Array| An array of the names of topics subscribed to by the group. If there is no such array, this parameter represents all the topic information in the specified group |
|searchWord| No |String| Fuzzy match by topicName |
|offset| No |Int| Offset of this query. Default value is 0 |
|limit | No |Int| Maximum number of results to be returned. Default value is 50. Maximum value is 50 |



## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
|data|JSON Array| Returned information of the consumer group |
|data::totalCount|Int| Number of topics that meets the search criteria |
|data::topicList|JSON Array| Array of topics subscribed to by users and each element is a json object |
|data::topicList::topic|String| topicName subscribed to by the group |
|data::topicList::partitions|JSON Array| Array of partitions in the topic, where each element is a json object |
|data::topicList::parititons::partition|Int| partitionId of the topic |
|data::topicList::partitions::offset|Int| Offset position submitted by the consumer |
|data::topicList::partitions::metadata|String| When the consumer submits a message, the metadata is passed in for other purposes. Currently, this is generally an empty string |
|data::topicList::partitions::log_end_offset|Int| Latest offset of the current partition |
|data::topicList::partitions::lag|Int| Number of unconsumed messages |

## 4. Samples
**Input:**
```http
 https://domain/v2/index.php?Action=GetGroupOffsets&<Common Request Parameters>
```

**Output:**
```
{
	"code": 0,
	"message": "",
	"codeDesc": "Success",
	"data": {
		"totalCount": 1,
		"topicList": [{
			"topic": "test",
			"partitions": [{
				"partition": 0,
				"offset": 22689638,
				"metadata": "",
				"err_code": 0,
				"log_end_offset": 207927929,
				"lag": 185238291
			}]
		}]
	}
}
```


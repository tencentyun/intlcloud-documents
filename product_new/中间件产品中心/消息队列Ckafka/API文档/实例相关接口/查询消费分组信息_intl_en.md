## 1. API Description

This API (ListConsumerGroup) is used to get CKafka consumer group information under the user account.

API domain name: `ckafka.api.qcloud.com`

## 2. Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/431/5883).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
|instanceId | No | String| (Filter) Filter by instance ID |
|groupName| No |String| Consumer group name (exact match) |
|topicName| No |String| Topic name. Parameter will be ignored if groupName is left empty |
|offset | No |Int| Offset. Default value is 0 if left empty |
|limit | No |Int| Number of results to be returned. Default value is 50 if left empty, and the maximum value is 50 |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| totalCount | Int | Number of consumer groups that meets the search criteria |
| groupList| json array object | Consumer group details. Refer to the output parameter description for definition |


## 4. Samples

**Input:**

```
 https://domain/v2/index.php?Action=ListConsumerGroup&<Common Request Parameters>
```

**Output:**

```
  {
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "totalCount": 1, // Number of consumer groups that meets the search criteria
        "topicList": {
            "tes": "topic-4imuy62g"
        },
        "groupList": { // Consumer group list
            "console-consumer-24193": { // Consumer group name
                "tes": [ // Key is the name of the topic subscribed to by this consumer group. The array represents the offset of consumption progress for each partition of the consumer group in the topic.
                    10,
                    12,
                    12,
                    12,
                    12,
                    12,
                    12,
                    11
                ]
            }
        },
        "totalPartition": 8,
        "partitionListForMonitor": [
            {
                "partitionId": 0
            },
            {
                "partitionId": 1
            },
            {
                "partitionId": 2
            },
            {
                "partitionId": 3
            },
            {
                "partitionId": 4
            },
            {
                "partitionId": 5
            },
            {
                "partitionId": 6
            },
            {
                "partitionId": 7
            }
        ],
        "totalTopic": 1,
        "topicListForMonitor": [
            {
                "topicName": "tes",
                "topicId": "topic-4imuy62g"
            }
        ],
        "groupListForMonitor": [
            {
                "groupName": "console-consumer-24193"
            }
        ]
    }
}
```


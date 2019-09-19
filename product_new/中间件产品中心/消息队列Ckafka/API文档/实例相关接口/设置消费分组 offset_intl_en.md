## 1. API Description

This API (SetGroupOffsets) is used to set the offset of a consumer group on a CKafka instance under the user account.

API domain name: `ckafka.api.qcloud.com`

## 2. Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/431/5883).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
|instanceId | Yes | String| (Filter) Filter by instance ID |
|group| Yes |String | CKafka consumer group |
|topics| No |String Array| An array of topics for which the offset needs to be reset. All topics will be reset if this is left empty |
|strategy| Yes |Int| Policy to reset the offset. Meanings of input parameters: <br> 0: Align the `shift-by` parameter, moving the offset forward or backward by the value of the `shift`. <br> 1: Align references (`by-duration`, `to-datetime`, `to-earliest`, or `to-latest`), moving the offset to a specified timestamp location. <br> 2: Align references (`to-offset`), moving the offset to a specified offset position |
|shift| No |Int| When `strategy` is 0, this field is required. If it is above zero, the offset will be shifted backward by the value of the `shift`. If it is below zero, the offset will be shifted forward by the value of the `shift`. After a correct reset, the new offset should be (old_offset + shift). **If the new offset is smaller than the `earliest` value of the partition, it will be set to the `earliest` value; if it is greater than the `latest` value of the partition, it will be set to the `latest` value** |
|timestamp| No |Int|Unit: ms. When `strategy` is 1, this field is required; -2 indicates that the offset is reset to the initial position and -1 indicates that the offset is reset to the latest position (equivalent to emptying). Other values represent the specified times where the offset of the topic will be obtained and then reset. **If there is no message at the specified time, the last offset will be obtained** |
|offset| No |Int| Position of the offset that needs to be reset. When `strategy` is 2, this field is required |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
|data|JSON Array| Consumer group configuration results returned by this API call |
|data::succ|JSON Array| Array of successful resets. See instances for details |
|data::failed|JSON Array| Array of failed resets. See instances for details |

## 4. Samples

Input:

```
 https://domain/v2/index.php?Action=SetGroupOffset&<Common Request Parameters>
```

Output:

```
{
    "codeDesc":"Success",
    "code":0,
    "msg":"",
    "data":{
        "succ":[
            {
                "topic":"streams-wordcount-output",// Topic name
                "error_code":0,
                "partitions":[
                    {
                        "partition":2, // Partition ID 
                        "offset":27708,// Partition offset
                        "error_code":0
                    },
                    {
                        "partition":1,
                        "offset":112843,
                        "error_code":0
                    },
                    {
                        "partition":3,
                        "offset":29149,
                        "error_code":0
                    },
                    {
                        "partition":0,
                        "offset":29402,
                        "error_code":0
                    }
                ]
            }
        ],
        "failed":[
            {
                "topic":"aaaa",// Topic name
                "error_code":3,
                "error_msg":"This request is for a topic or partition that does not exist on this broker.",// Error message
                "partitions":[
                ]
            }
        ]
    }
}
```


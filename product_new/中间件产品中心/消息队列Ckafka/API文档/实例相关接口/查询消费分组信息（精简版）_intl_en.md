## 1. API Description

This API (ListGroup) is used to get CKafka consumer group information under the user account. This lite API returns less consumer group information. You can call the GetGroupInfo API to query consumer group details.

API domain name: `ckafka.api.qcloud.com`

## 2. Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/doc/api/431/5883).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
|instanceId | No | String| (Filter) Filter by instance ID |
|group| No |String| Consumer group (exact match) |
|searchWord| No |String| Fuzzy match by group |
|offset | No |Int| Offset. Default value is 0 if left empty |
|limit | No |Int| Number of results to be returned. Default value is 20 if left empty. The maximum value is 50 |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
|totalCount | Int | Number of eligible consumer groups |
|groupList| JSON Array Object | Consumer group details. Please refer to the output parameter description for definition |
|groupList::group|String |groupId |
|groupList::protocol|String| Protocol used by this group |


## 4. Samples

Input:

```
 https://domain/v2/index.php?Action=ListGroup&<Common Request Parameters>
```

Output:

```
 {
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "totalCount": 1, // Number of groups that meets the search criteria
        "groupList": [
            {
                "group": "mirror_vpc_forward",// groupId
                "protocol": "consumer" // The protocol used by this group
            }
        ]
    }
}
```


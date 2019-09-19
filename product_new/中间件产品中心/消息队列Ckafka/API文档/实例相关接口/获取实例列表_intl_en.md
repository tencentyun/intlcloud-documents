## 1. API Description
API domain name: `ckafka.api.qcloud.com`
This API (ListInstance) is used to get the list of CKafka instances under the user account.


## 2. Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/597/10084).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| instanceId | No | String| (Filter) Filter by instance ID |
| searchWord | No | String | (Filter) Filter by instance name. Fuzzy search is supported |
|status.n | No |Int| (Filter) Instance status. 0: Creating; 1: Running; 2: Deleting. All instances are returned by default if this parameter is left empty |
|offset | No |Int| Offset. Default value is 0 if left empty |
|limit | No |Int| Number of results to be returned. Default value is 10 if left empty, and the maximum value is 20 |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| totalCount | Int | Number of eligible instances |
| instanceList | Array | List of instance information |
| instanceList::instanceId | String| Instance ID |
| instanceList::instanceName | String| Instance name |
| instanceList::status | Int | Instance status. 0: Creating; 1: Running; 2: Deleting |

## 4. Samples

Input:

```
 https://domain/v2/index.php?Action=ListInstance&<Common Request Parameters>
```

Output:

```
  {
      "code" : 0,
      "message" : "ok",
	"codeDesc":"Success",
	"totalCount": 14,
     "instanceList": [
        {
            "instanceId":"ckafka-xxooa0",
		"instanceName":"test",
		"status":0
        }
    ]
  }

```







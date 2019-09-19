## 1. API Description
API domain name: `ckafka.api.qcloud.com`
This API (CleanLog) is used to delete logs.


## 2. Input Parameters

The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/597/10084).

| Parameter Name | Required | Type | Description |
| --- | --- | --- | --- |
| instanceId | Yes | String | Instance ID |
 cleanStrategy | Yes | Int | Required. Methods to delete old data. 1: Delete data before the specified offset; 2: Delete data before the specified time |
| startOffset | No | Int | Required when cleanStrategy=1. Delete data before startOffset in the specified topic-partition |
| startTimeStamp | No | Int | Required when cleanStrategy=2. Delete data before startTimeStamp. Users can specify the topic |
| topicName | No | String | Required when cleanStrategy = 1. Optional when cleanStrategy = 2 |
| partition | No | Int | Required when cleanStrategy = 1 |

## 3. Samples

Input:

```
 https://domain/v2/index.php?Action=CleanLog&instanceId=ckafka-xxooa0&cleanStrategy=1&<Common Request Parameters>
```

Output:

```
{
	"code": 0,
	"codeDesc": "Success",
	"message": "ok"
}
```

## 1. API Description
This API (GetMongoDBJobInfo) is used to query the execution status of a task.
API domain name: **mongodb.api.qcloud.com**.

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/213/6976). The Action field of this API is `GetMongoDBJobInfo`.

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| jobId | Yes | String | The task ID returned when the task is executed |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/377/8946). |
| message | String | Error message. A null value indicates a success |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned.|
| data | Object | The execution result of the task |

`data` indicates the task execution result and is composed as follows:

| Parameter Name | Type | Description |
|:---------|---------|---------|
| data.status | Int | Task status. 0: to be executed; 1: executing, 2: succeeded; 3: failed; -1: execution error |

## 4. Error Codes
The following lists the error codes related to this API.

| Error Code | Error Message | Error Description |
|---------|---------|---------|
| 11050 | InvalidParameter | Invalid service parameter. |


## 5. Samples
<pre>
https://mongodb.api.qcloud.com/v2/index.php?Action=GetMongoDBJobInfo
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common request parameter</a>>
&jobId=11963
</pre>
Below is a sample return:
```
{
    "code": 0,
	"message": "",
	"codeDesc": "Success",
    "data": {
        "status": 2
    }
}
```
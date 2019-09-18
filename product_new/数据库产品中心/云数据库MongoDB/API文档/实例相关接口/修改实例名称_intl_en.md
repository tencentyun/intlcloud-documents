## 1. API Description
This API (ModifyMongoDBName) is used to rename an instance.
API domain name: **mongodb.api.qcloud.com**.

Instance name rule: It can contain 1-36 letters, digits, English punctuation marks, _, or -

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/213/6976). The Action field of this API is ModifyMongoDBName.

| Parameter Name | Required | Type | Description |
|:---------|---------|---------|---------|
| instanceId | Yes | String | The ID of the instance to be operated on, which can be obtained from the `instanceId` field in the return value of the [DescribeMongoDBInstances API](https://intl.cloud.tencent.com/document/product/240/8312). |
| instanceName | Yes | String | The name of the instance. It can contain 1-36 letters, digits, English punctuation marks, _, or - |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/377/8946). |
| message | String | Error message. A null value indicates a success |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned.|

## 4. Error Codes
The following lists the error codes related to this API.

| Error Code | Error Message | Error Description |
|---------|---------|---------|
| 11050 | InvalidParameter | Invalid service parameter. |
|11056|InstanceNotExists| No corresponding instance was found. |
|11051|InstanceDeleted| The instance has been repossessed upon expiration. |
|11052|InstanceIsolated| The instance has been isolated upon expiration. |
|11054|InstanceNameExceedMaxLimit| The instance name length exceeds the upper limit. |
|11055|InstanceNameRuleError| The instance name is in the incorrect format. It can only contain 1-36 letters, digits, English punctuation marks, _, or - |


## 5. Samples
<pre>
https://mongodb.api.qcloud.com/v2/index.php?Action=ModifyMongoDBName
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common request parameter</a>>
&instanceId=cmgo-6ozqe0uh
&instanceName=test_API
</pre>
Below is a sample return:
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success"
}

```
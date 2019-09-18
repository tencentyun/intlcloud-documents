## 1. API Description
This API (ResetMongoDBPassword) is used to reset the password for an instance.
API domain name: **mongodb.api.qcloud.com**.

Password rule: It can only contain 8-16 characters and must contain at least two of the following types of characters: letters, digits, and special characters (!@#%^()).

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/213/6976). The Action field of this API is ResetMongoDBPassword.

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| instanceId | Yes | String | The ID of the instance to be operated on, which can be obtained from the `instanceId` field in the return value of the [DescribeMongoDBInstances API](https://intl.cloud.tencent.com/document/product/240/8312). |
| password | Yes | String | The new password for the instance. It can only contain 8-16 characters and must contain at least two of the following types of characters: letters, digits, and special characters (!@#%^()) |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/377/8946). |
| message | String | Error message. A null value indicates a success |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |
| data | Object | The ID of the task |

`data` indicates the ID of the task and is composed as follows:

| Parameter Name | Type | Description |
|---------|---------|---------|
| data.jobId | Int | The ID of the task, which can be used to query the task execution condition through the [GetMongoDBJobInfo API](https://intl.cloud.tencent.com/document/product/240/8310) |


## 4. Error Codes
The following lists the error codes related to this API.

| Error Code | Error Message | Error Description |
|---------|---------|---------|
| 11050 | InvalidParameter | Invalid service parameter. |
|11056|InstanceNotExists| No corresponding instance was found. |
| 11057 | InstanceBeenLocked | Unable to execute operation because the instance is locked by another process |
| 10702 | InstanceStatusAbnormal | Unable to execute operation due to an abnormal instance status. For example, the instance’s status is "in process" or "isolated" or "deleted" |
|11059|PasswordRuleError| Password rule error. Passwords can only contain 8-16 characters and must contain at least two of the following types of characters: letters, digits, and special characters (!@#%^*()) |

## 5. Samples
<pre>
https://mongodb.api.qcloud.com/v2/index.php?Action=ResetMongoDBPassword
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common request parameter</a>>
&instanceId=cmgo-6ozqe0uh
&password=12D3E@!r5ed
</pre>
Below is a sample return:
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "jobId": 73605
    }
}

```
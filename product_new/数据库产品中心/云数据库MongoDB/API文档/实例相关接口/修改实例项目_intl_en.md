## 1. API Description 
This API (ModifyMongoDBProject) is used to modify the project to which an instance belongs.
API domain name: **mongodb.api.qcloud.com**.

## 2. Input Parameters
Below is a list of API request parameters. You need to add common request parameters to your request when calling this API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/213/6976). The Action field of this API is ModifyMongoDBProject.

| Parameter Name | Required | Type | Description |
|:---------|---------|---------|---------|
| instanceIds.n | No | String | One or more instance IDs. n represents an array subscript starting from 0. Instance ID can be obtained from the `instanceId` field in the return value of the [DescribeMongoDBInstances API](https://intl.cloud.tencent.com/document/product/240/8312). |
| projectId | Yes | Int | Project ID. The value is subject to the projectId returned by User Account > User Account API Query > [Project List](https://intl.cloud.tencent.com/document/product/378/4400) |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| code | Int | Common error code. 0: success; other values: failure. For more information, see [Common Error Codes](https://cloud.tencent.com/doc/api/372/%E9%94%99%E8%AF%AF%E7%A0%81#1.E3.80.81.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81). |
| message | String | Error message. A null value indicates a success |
| codeDesc | String | Description of the action status. When the action has succeeded, "Success" is returned. When the action has failed, a message describing the cause of the error is returned. |

## 4. Error Codes
The following lists the error codes related to this API.

| Error Code | Error Message | Error Description |
|---------|---------|---------|
| 11050 | InvalidParameter | Invalid service parameter. |
|11056|InstanceNotExists| No corresponding instance was found. |
| 11057 | InstanceBeenLocked | Unable to execute operation because the instance is locked by another process |
| 10702 | InstanceStatusAbnormal | Unable to execute operation due to an abnormal instance status. For example, the instance’s status is "in process" or "isolated" or "deleted" |

## 5. Samples
<pre>
  https://mongodb.api.qcloud.com/v2/index.php?Action=ModifyMongoDBProject
	&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">Common request parameter</a>>
	&instanceIds.0=cmgo-6ozqe0uh
	&projectId=1001
</pre>
Below is a sample return:
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success"
}

```
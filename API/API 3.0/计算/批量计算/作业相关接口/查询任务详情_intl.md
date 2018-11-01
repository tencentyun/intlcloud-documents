## **1. API Description**
API request domain name: batch.tencentcloudapi.com.

This API is used to query the details of a specified task, including information about the task instances inside the task.

Default API request frequency limit: 2 times/second.



## **2. Input Parameters**

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/599/15883).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeTask |
| Version | Yes | String | Common parameter; the value for this API: 2017-03-12 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/599/15883#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| JobId | Yes | String | Job ID |
| TaskName | Yes | String | Task name |

## **3. Output Parameters**

| Parameter name | Type | Description |
|---------|---------|---------|
| JobId | String | Job ID|
| TaskName | String | Task name |
| TaskState | String | Task state |
| CreateTime | String | Created Time |
| EndTime | String | End time |
| TaskInstanceTotalCount | Integer | Total number of task instances |
| TaskInstanceSet | Array of [TaskInstanceView](/document/api/599/15912#TaskInstanceView) | Task instance information |
| TaskInstanceMetrics | [TaskInstanceMetrics](/document/api/599/15912#TaskInstanceMetrics) | Task instance statistical metrics |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Querying Task Details

#### Input

```
https://batch.tencentcloudapi.com/?Action=DescribeTask
&JobId=job-97zcl3wt
&TaskName=A
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "CreateTime": "2018-02-07T09:29:09Z",
    "EndTime": "2018-02-07T09:30:31Z",
    "JobId": "job-97zcl3wt",
    "RequestId": "f4723b24-e080-4599-b12d-b7eb657faefe",
    "TaskInstanceMetrics": {
      "FailedCount": 0,
      "FailedInterruptedCount": 0,
      "PendingCount": 0,
      "RunnableCount": 0,
      "RunningCount": 0,
      "StartingCount": 0,
      "SubmittedCount": 0,
      "SucceedCount": 2
    },
    "TaskInstanceSet": [
      {
        "ComputeNodeInstanceId": null,
        "CreateTime": "2018-02-07T09:29:09Z",
        "EndTime": "2018-02-07T09:30:23Z",
        "ExitCode": 0,
        "LaunchTime": "2018-02-07T09:29:09Z",
        "RedirectInfo": {
          "StderrRedirectFileName": "stderr.job-97zcl3wt.A.1.log",
          "StderrRedirectPath": "cos://dondonbatch-1251783334.cosgz.myqcloud.com/hello2/logs/",
          "StdoutRedirectFileName": "stdout.job-97zcl3wt.A.1.log",
          "StdoutRedirectPath": "cos://dondonbatch-1251783334.cosgz.myqcloud.com/hello2/logs/"
        },
        "RunningTime": "2018-02-07T09:29:55Z",
        "StateIfCreateCvmFailed": "FAILED",
        "StateReason": "",
        "TaskInstanceIndex": 1,
        "TaskInstanceState": "SUCCEED"
      },
      {
        "ComputeNodeInstanceId": null,
        "CreateTime": "2018-02-07T09:29:09Z",
        "EndTime": "2018-02-07T09:30:31Z",
        "ExitCode": 0,
        "LaunchTime": "2018-02-07T09:29:09Z",
        "RedirectInfo": {
          "StderrRedirectFileName": "stderr.job-97zcl3wt.A.0.log",
          "StderrRedirectPath": "cos://dondonbatch-1251783334.cosgz.myqcloud.com/hello2/logs/",
          "StdoutRedirectFileName": "stdout.job-97zcl3wt.A.0.log",
          "StdoutRedirectPath": "cos://dondonbatch-1251783334.cosgz.myqcloud.com/hello2/logs/"
        },
        "RunningTime": "2018-02-07T09:30:02Z",
        "StateIfCreateCvmFailed": "FAILED",
        "StateReason": "",
        "TaskInstanceIndex": 0,
        "TaskInstanceState": "SUCCEED"
      }
    ],
    "TaskInstanceTotalCount": 2,
    "TaskName": "A",
    "TaskState": "SUCCEED"
  }
}
```


## 5. Developer Resources

**It is recommended to use [`API 3.0 Explorer`](https://console.cloud.tencent.com/api/explorer). This tool provides various capabilities such as online debugging, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

Cloud API 3.0 comes with a set of complementary development tools that make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/599/15885#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameter.JobIdMalformed | Invalid job ID format. |
| ResourceNotFound.Task | The specified job task does not exist. |


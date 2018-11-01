## **1. API Description**
API request domain name: batch.tencentcloudapi.com.

This API is used to view the detailed information about a job, including internal task (Task) and dependency (Dependence) information.

Default API request frequency limit: 2 times/second.



## **2. Input Parameters**

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/599/15883).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeJob |
| Version | Yes | String | Common parameter; the value for this API: 2017-03-12 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/599/15883#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| JobId | Yes | String | Job ID |

## **3. Output Parameters**

| Parameter name | Type | Description |
|---------|---------|---------|
| JobId | String | Job ID|
| JobName | String | Job name |
| Zone | String | Availability zone information |
| Priority | Integer | Job priority |
| JobState | String | Job state |
| CreateTime | String | Created Time |
| EndTime | String | End time |
| TaskSet | Array of [TaskView](/document/api/599/15912#TaskView) | Task view information |
DependenceSet | Array of [Dependence](/document/api/599/15912#Dependence) | Information about the dependency among tasks |
| TaskMetrics | [TaskMetrics](/document/api/599/15912#TaskMetrics) | Task statistical metrics |
| TaskInstanceMetrics | [TaskInstanceView](/document/api/599/15912#TaskInstanceView) | Task instance statistical metrics |
| StateReason | String | Reason for job failure |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Querying Job Details

#### Input

```
https://batch.tencentcloudapi.com/?Action=DescribeJob
&JobId=job-97zcl3wt
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "CreateTime": "2018-02-07T09:29:09Z",
    "DependenceSet": [
      {
        "EndTaskName": "B",
        "StartTaskName": "A"
      },
      {
        "EndTaskName": "C",
        "StartTaskName": "A"
      },
      {
        "EndTaskName": "D",
        "StartTaskName": "B"
      },
      {
        "EndTaskName": "D",
        "StartTaskName": "C"
      }
    ],
    "EndTime": "2018-02-07T09:33:01Z",
    "JobId": "job-97zcl3wt",
    "JobName": "test job",
    "JobState": "SUCCEED",
    "Priority": 1,
    "RequestId": "d1b08863-b8ee-49d4-aa08-f464499f97a0",
    "TaskInstanceMetrics": {
      "FailedCount": 0,
      "FailedInterruptedCount": 0,
      "PendingCount": 0,
      "RunnableCount": 0,
      "RunningCount": 0,
      "StartingCount": 0,
      "SubmittedCount": 0,
      "SucceedCount": 8
    },
    "TaskMetrics": {
      "FailedCount": 0,
      "FailedInterruptedCount": 0,
      "PendingCount": 0,
      "RunnableCount": 0,
      "RunningCount": 0,
      "StartingCount": 0,
      "SubmittedCount": 0,
      "SucceedCount": 4
    },
    "TaskSet": [
      {
        "CreateTime": "2018-02-07T09:29:09Z",
        "EndTime": "2018-02-07T09:30:31Z",
        "TaskName": "A",
        "TaskState": "SUCCEED"
      },
      {
        "CreateTime": "2018-02-07T09:29:09Z",
        "EndTime": "2018-02-07T09:31:49Z",
        "TaskName": "B",
        "TaskState": "SUCCEED"
      },
      {
        "CreateTime": "2018-02-07T09:29:09Z",
        "EndTime": "2018-02-07T09:31:48Z",
        "TaskName": "C",
        "TaskState": "SUCCEED"
      },
      {
        "CreateTime": "2018-02-07T09:29:09Z",
        "EndTime": "2018-02-07T09:33:01Z",
        "TaskName": "D",
        "TaskState": "SUCCEED"
      }
    ],
    "Zone": "ap-guangzhou-2"
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

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/599/15885#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameter.JobIdMalformed | Invalid job ID format. |
| ResourceNotFound.Job | The specified job does not exist. |


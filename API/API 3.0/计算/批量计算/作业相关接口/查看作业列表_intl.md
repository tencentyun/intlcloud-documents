## **1. API Description**
API request domain name: batch.tencentcloudapi.com.

This API used to query the overview information of several jobs

Default API request frequency limit: 2 times/second.



## **2. Input Parameters**

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/599/15883).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeJobs |
| Version | Yes | String | Common parameter; the value for this API: 2017-03-12 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/599/15883#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| JobIds.N | No | Array of String | Job ID |
| Filters.N | No | Array of [Filter](/document/api/599/15912#Filter) | Filter |
| Offset | No | Integer | Offset |
| Limit | No | Integer | Number of returns |

## **3. Output Parameters**

| Parameter name | Type | Description |
|---------|---------|---------|
| JobSet | [JobView](/document/api/599/15912#JobView) | Job list |
| TotalCount | Integer | Number of eligible jobs |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Querying Job Information

#### Input

```
https://batch.tencentcloudapi.com/?Action=DescribeJobs
&JobIds.0=job-97zcl3wt
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "JobSet": [
      {
        "CreateTime": "2018-02-07T09:29:09Z",
        "EndTime": "2018-02-07T09:33:01Z",
        "JobId": "job-97zcl3wt",
        "JobName": "test job",
        "JobState": "SUCCEED",
        "Placement": {
          "Zone": "ap-guangzhou-2"
        },
        "Priority": 1,
        "TaskMetrics": {
          "FailedCount": 0,
          "FailedInterruptedCount": 0,
          "PendingCount": 0,
          "RunnableCount": 0,
          "RunningCount": 0,
          "StartingCount": 0,
          "SubmittedCount": 0,
          "SucceedCount": 4
        }
      }
    ],
    "RequestId": "c76c5368-6e2d-46bc-9867-5a3019510b76",
    "TotalCount": 1
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
| InvalidParameterValue | Invalid parameter value. |
| InvalidZone.MismatchRegion | The specified zone does not exist. |
| UnknownParameter | Unknown parameter error |


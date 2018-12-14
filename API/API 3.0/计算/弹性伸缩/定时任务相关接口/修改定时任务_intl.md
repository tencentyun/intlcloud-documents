## 1. API Description

Domain name for API request: as.tencentcloudapi.com.

This API (ModifyScheduledAction) is used to modify a scheduled task.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter `Region` is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value ​used for this API: ModifyScheduledAction |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| ScheduledActionId | Yes | String | ID of the scheduled task to be modified |
| ScheduledActionName | No | String | Scheduled task name, which is unique under one scaling group. It can contain up to 60 characters, including letters, numbers, underscores, hyphens ("-") and decimal points. |
| MaxSize | No | Integer | The upper limit of instances that triggers a scheduled task |
| MinSize | No | Integer | The lower limit of instances that triggers a scheduled taskd |
| DesiredCapacity | No | Integer | The desired number of instances when a scheduled task is triggered |
| StartTime | No | Timestamp | Time when the scheduled task is triggered for the first time, which is based on Beijing Time (UTC+8) and in the `ISO8601` format, such as `YYYY-MM-DDThh:mm:ss+08:00`. |
| EndTime | No | Timestamp | End time for the scheduled task, which is based on `Beijing Time` (UTC+8) and in the `ISO8601` format, such as `YYYY-MM-DDThh:mm:ss+08:00`.<br> It must be used together with `Recurrence`. The scheduled task will be invalid after the specified end time. |
| Recurrence | No | String | Repetition mode of the scheduled task, which is in the [Cron](https://zh.wikipedia.org/wiki/Cron) format.<br>It must be used together with `EndTime`. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Modify a scheduled task

#### Input

```
https://as.tencentcloudapi.com/?Action=ModifyScheduledAction
&ScheduledActionId=asst-chwbkq4c
&ScheduledActionName=scheduled-action-0
&MaxSize=5
&MinSize=0
&DesiredCapacity=3
&StartTime=2018-08-28T23:00:00+08:00
&<Common request parameters>
```

#### Output

```
{
  "Response": {
    "RequestId": "5f6f0f95-216f-4745-a2e6-617897e9cedb"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using Tencent Cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyScheduledAction)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameterValue.CronExpressionIllegal | The Cron expression specified in the scheduled task is invalid |
| InvalidParameterValue.EndTimeBeforeStartTime | The end time set for the scheduled task is earlier than the start time |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | Invalid characters in the scheduled task name |
| InvalidParameterValue.ScheduledActionNameDuplicate | Duplicate scheduled task names |
| InvalidParameterValue.Size | The desired, maximum and minimum numbers of instances are invalid |
| InvalidParameterValue.StartTimeBeforeCurrentTime | The start time set for the scheduled task is earlier than the current time |
| InvalidParameterValue.TimeFormat | Invalid time format |
| InvalidParameterValue.TooLong | Too many parameter values |
| LimitExceeded.DesiredCapacityLimitExceeded | The desired number of instances exceeds the limit |
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the upper limit |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances falls below the lower limit |
| LimitExceeded.ScheduledActionLimitExceeded | The number of scheduled tasks exceeds the limit |
| ResourceNotFound.ScheduledActionNotFound | The specified scheduled task does not exist |


## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (ModifyScheduledAction) is used to modify a scheduled action.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: ModifyScheduledAction |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| ScheduledActionId | Yes | String | ID of the scheduled action to be edited |
| ScheduledActionName | No | String | Scheduled action name, which is unique under one auto scaling group. It can only contain letters, numbers, underscores, hyphens ("-") and decimal points. Its length cannot exceed 60 characters. |
| MaxSize | No | Integer | The maximum number of instances in the auto scaling group when a scheduled action is triggered |
| MinSize | No | Integer | The minimum number of instances in the auto scaling group when a scheduled action is triggered |
| DesiredCapacity | No | Integer | The desired number of instances when a scheduled action is triggered |
| StartTime | No | Timestamp | Time when the scheduled action is triggered for the first time, which is based on Beijing Time (UTC+8) and in the format of `YYYY-MM-DDThh:mm:ss+08:00` according to the `ISO8601` standard. |
| EndTime | No | Timestamp | The end time of the scheduled action. The value is in `Beijing time` (UTC+8) in the format of `YYYY-MM-DDThh:mm:ss+08:00` according to the `ISO8601` standard. <br>This parameter and `Recurrence` need to be specified at the same time. After the end time, the scheduled action will no longer take effect. |
| Recurrence | No | String | The repeating mode of the scheduled action, which is in standard [Cron](https://zh.wikipedia.org/wiki/Cron) format. <br>This parameter and `EndTime` need to be specified at the same time. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Modifying a Scheduled Action

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=ModifyScheduledAction
&ScheduledActionId=asst-chwbkq4c
&ScheduledActionName=scheduled-action-0
&MaxSize=5
&MinSize=0
&DesiredCapacity=3
&StartTime=2018-08-28T23:00:00+08:00
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "5f6f0f95-216f-4745-a2e6-617897e9cedb"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyScheduledAction)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameterValue.CronExpressionIllegal | The Cron expression specified in the scheduled action is invalid |
| InvalidParameterValue.EndTimeBeforeStartTime | The end time set for the scheduled action is earlier than the start time |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | Invalid characters in the scheduled action name |
| InvalidParameterValue.ScheduledActionNameDuplicate | The scheduled action name already exists. |
| InvalidParameterValue.Size | The value of maximum, minimum, or desired number of instances in the auto scaling group is invalid. |
| InvalidParameterValue.StartTimeBeforeCurrentTime | The start time of the scheduled action is before the current time. |
| InvalidParameterValue.TimeFormat | Invalid time format. |
| InvalidParameterValue.TooLong | Too many parameter values. |
| LimitExceeded.DesiredCapacityLimitExceeded | The desired number of instances exceeds the limit |
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the upper limit |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances falls below the lower limit |
| LimitExceeded.ScheduledActionLimitExceeded | The number of scheduled actions exceeds the limit |
| ResourceNotFound.ScheduledActionNotFound | The specified scheduled action does not exist. |

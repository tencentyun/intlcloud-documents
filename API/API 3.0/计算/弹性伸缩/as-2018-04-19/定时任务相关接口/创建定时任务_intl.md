## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (CreateScheduledAction) is used to create a scheduled action.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreateScheduledAction |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingGroupId | Yes | String | Auto scaling group ID |
| ScheduledActionName | Yes | String | Scheduled action name, which is unique under one auto scaling group. It can only contain letters, numbers, underscores, hyphens ("-") and decimal points. Its length cannot exceed 60 characters. |
| MaxSize | Yes | Integer | The maximum number of instances in the auto scaling group when a scheduled action is triggered |
| MinSize | Yes | Integer | The minimum number of instances in the auto scaling group when a scheduled action is triggered |
| DesiredCapacity | Yes | Integer | The desired number of instances in the auto scaling group when a scheduled action is triggered |
| StartTime | Yes | Timestamp | Time when the scheduled action is triggered for the first time, which is based on Beijing Time (UTC+8) and in the `ISO8601` format, such as `YYYY-MM-DDThh:mm:ss+08:00`. |
| EndTime | No | Timestamp | The end time of the scheduled action. The value is in `Beijing time` (UTC+8) in the format of `YYYY-MM-DDThh:mm:ss+08:00` according to the `ISO8601` standard. <br><br>This parameter and `Recurrence` need to be specified at the same time. After the end time, the scheduled action will no longer take effect. |
| Recurrence | No | String | The repeating mode of the scheduled action, which is in standard [Cron](https://zh.wikipedia.org/wiki/Cron) format. <br><br>This parameter and `EndTime` need to be specified at the same time. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| ScheduledActionId | String | Scheduled action ID |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Creating a Single-run Scheduled Action

This is to create a scheduled action to adjust the maximum, minimum, and desired numbers of instances in the auto scaling group to 10, 4, and 6 respectively at 23:00, August 28, 2018.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateScheduledAction
&AutoScalingGroupId=asg-2nr9xh8h
&ScheduledActionName=scheduled-action-0
&MaxSize=10
&MinSize=4
&DesiredCapacity=6
&StartTime=2018-08-28T23:00:00+08:00
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "ScheduledActionId": "asst-chwbkq4c",
    "RequestId": "193a710f-8dbf-46aa-8b4a-195532244df8"
  }
}
```

### Sample 2. Creating a Recurring Scheduled Action

This is to create a scheduled action to adjust the maximum, minimum, and desired numbers of instances in the auto scaling group to 7, 2, and 3 respectively at 23:00 everyday starting August 28, 2018 and ending at 00:00, January 1, 2019.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateScheduledAction
&AutoScalingGroupId=asg-2nr9xh8h
&ScheduledActionName=scheduled-action-1
&MaxSize=7
&MinSize=2
&DesiredCapacity=3
&StartTime=2018-08-28T23:00:00+08:00
&EndTime=2019-01-01T00:00:00+08:00
&Recurrence=0 23 */1 * *
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "ScheduledActionId": "asst-le3us530",
    "RequestId": "502fd6fa-44ff-4c79-b77e-ee20f72bddc0"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateScheduledAction)

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
| MissingParameter | Missing parameter. |
| ResourceNotFound.AutoScalingGroupIdNotFound | The auto scaling group does not exist |

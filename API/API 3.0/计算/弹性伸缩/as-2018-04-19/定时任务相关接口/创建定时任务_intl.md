## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (CreateScheduledAction) creates a scheduled action.

Default API request frequency limit: 20 times/second.

Note: Because financial availability zones and non-financial availability zones are isolated. When specifying a financial availability zone (e.g., ap-shanghai-fsi) in the Region (a common parameter), you should also choose the financial availability zone preferably in the same region as that one specified in Region for the domain, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/377/20426).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: CreateScheduledAction |
| Version | Yes | String | Common parameter; the version this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| AutoScalingGroupId | Yes | String | Scaling group ID |
| ScheduledActionName | Yes | String | Scheduled action name. The name can contain Chinese characters, letters, numbers, underscores, separators ("-"), and decimal points with a maximum length of 60 bytes. It must be unique in the same scaling group. |
| MaxSize | Yes | Integer | The maximum number of instances set for the scaling group when the scheduled action is triggered. |
| MinSize | Yes | Integer | The minimum number of instances set for the scaling group when the scheduled action is triggered. |
| DesiredCapacity | Yes | Integer | The desired number of instances set for the scaling group when the scheduled action is triggered. |
| StartTime | Yes | Timestamp | The initial triggering time of the scheduled action. The value is in `Beijing time` (UTC+8) in the format of `YYYY-MM-DDThh:mm:ss+08:00` according to the `ISO8601` standard. |
| EndTime | No | Timestamp | The end time of the scheduled action. The value is in `Beijing time` (UTC+8) in the format of `YYYY-MM-DDThh:mm:ss+08:00` according to the `ISO8601` standard. <br><br>This parameter and `Recurrence` need to be specified at the same time. After the end time, the scheduled action will no longer take effect. |
| Recurrence | No | String | The repeating mode of the scheduled action. It is in standard [cron](https://zh.wikipedia.org/wiki/Cron) format. <br><br>This parameter and `EndTime` need to be specified at the same time. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| ScheduledActionId | String | Scheduled action ID |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues |

## 4. Sample

### Creating a Single-run Scheduled Action

This is to create a scheduled action to adjust the maximum, minimum, and desired numbers of instances in the scaling group to 10, 4, and 6 respectively at 23:00, August 28, 2018).

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

### Creating a Recurring Scheduled Action

This is to create a scheduled action to adjust the maximum, minimum, and desired numbers of instances in the scaling group to 7, 2, and 3 respectively at 23:00 everyday starting August 28, 2018 and ending at 00:00, January 1, 2019.

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

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateScheduledAction)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes,  see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameterValue.CronExpressionIllegal | The cron expression specified for the scheduled action is invalid. |
| InvalidParameterValue.EndTimeBeforeStartTime | The end time of the scheduled action is before the start time. |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | The scheduled action name contains invalid characters. |
| InvalidParameterValue.ScheduledActionNameDuplicate | The scheduled action name already exists. |
| InvalidParameterValue.Size | The value of maximum, minimum, or the desired number of instances is invalid. |
| InvalidParameterValue.StartTimeBeforeCurrentTime | The start time of the scheduled action is before the current time. |
| InvalidParameterValue.TimeFormat | Wrong time format. |
| InvalidParameterValue.TooLong | Too many values. |
| LimitExceeded.DesiredCapacityLimitExceeded | The desired number of instances exceeds the limit. |
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the limit. |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances is below the limit. |
| LimitExceeded.ScheduledActionLimitExceeded | The number of scheduled actions exceeds the limit. |
| MissingParameter | Missing parameter |
| ResourceNotFound.AutoScalingGroupIdNotFound | The scaling group does not exist. |

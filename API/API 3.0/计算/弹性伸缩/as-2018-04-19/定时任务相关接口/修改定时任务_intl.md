## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (ModifyScheduledAction) is used to modify a scheduled action.

Default API request frequency limit: 20 times/second.

Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/377/20426).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: ModifyScheduledAction |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| ScheduledActionId | Yes | String | ID of the scheduled action to edit |
| ScheduledActionName | No | String | Scheduled action name. The name can contain Chinese characters, letters, numbers, underscores, separators ("-"), and decimal points with a maximum length of 60 bytes. It must be unique in the same scaling group. |
| MaxSize | No | Integer | The maximum number of instances set for the scaling group when the scheduled action is triggered. |
| MinSize | No | Integer | The minimum number of instances set for the scaling group when the scheduled action is triggered. |
| DesiredCapacity | No | Integer | The desired number of instances set for the scaling group when the scheduled action is triggered. |
| StartTime | No | Timestamp | The initial triggering time of the scheduled action. The value is in `Beijing time` (UTC+8) in the format of `YYYY-MM-DDThh:mm:ss+08:00` according to the `ISO8601` standard. |
| EndTime | No | Timestamp | The end time of the scheduled action. The value is in `Beijing time` (UTC+8) in the format of `YYYY-MM-DDThh:mm:ss+08:00` according to the `ISO8601` standard. <br>This parameter and `Recurrence` need to be specified at the same time. After the end time, the scheduled action will no longer take effect. |
| Recurrence | No | String | The repeating mode of the scheduled action. It is in standard [cron](https://zh.wikipedia.org/wiki/Cron) format. <br>This parameter and `EndTime` need to be specified at the same time. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Modifying a Scheduled Action

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

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=ModifyScheduledAction)

### SDK

TencentCloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameterValue.CronExpressionIllegal | The cron expression specified for the scheduled action is invalid. |
| InvalidParameterValue.EndTimeBeforeStartTime | The end time of the scheduled action is before the start time. |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | The scheduled action name contains invalid characters. |
| InvalidParameterValue.ScheduledActionNameDuplicate | The scheduled action name already exists. |
| InvalidParameterValue.Size | The value of maximum, minimum, or desired number of instances is invalid. |
| InvalidParameterValue.StartTimeBeforeCurrentTime | The start time of the scheduled action is before the current time. |
| InvalidParameterValue.TimeFormat | Wrong time format. |
| InvalidParameterValue.TooLong | Too many values. |
| LimitExceeded.DesiredCapacityLimitExceeded | The desired number of instances exceeds the limit. |
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the limit. |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances is below the limit. |
| LimitExceeded.ScheduledActionLimitExceeded | The number of scheduled actions exceeds the limit. |
| ResourceNotFound.ScheduledActionNotFound | The specified scheduled action does not exist. |

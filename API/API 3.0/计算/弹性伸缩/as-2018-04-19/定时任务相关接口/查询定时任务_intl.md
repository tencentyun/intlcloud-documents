## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (DescribeScheduledActions) is used to query the details of one or more scheduled actions.

* You can query the details of scheduled actions based on information such as scheduled action ID, scheduled action name, or scaling group ID. For more information about filters, see `Filter`.
* If the parameter is empty, a certain number of scheduled actions (specified by Limit and 20 by default) of the current user is returned.

Default API request frequency limit: 20 times/second.

Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/377/20426).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeScheduledActions |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| ScheduledActionIds.N | No | Array of String | Query by one or more scheduled action IDs. Instance ID example: asst-am691zxo. The maximum number of instances per request is 100. The parameter does not support specifying both ScheduledActionIds and Filters at the same time. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter. <br/><li> scheduled-action-id - String - Required: No - (Filter) Filter by scheduled action ID. </li><li> scheduled-action-name - String - Required: No - (Filter) Filter by scheduled action name. </li><li> auto-scaling-group-id - String - Required: No - (Filter) Filter by scaling group ID. </li> |
| Offset | No | Integer | Offset, 0 by default. For more information about Offset, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |
| Limit | No | Integer | Number of returned results, 20 by default, up to 100. For more information about Limit, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of eligible scheduled actions. |
| ScheduledActionSet | Array of [ScheduledAction](/document/api/377/20453#ScheduledAction) | List of scheduled action details. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Querying a Scheduled Action

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeScheduledActions
&ScheduledActionIds.0=asst-caa5ha40
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "TotalCount": 1,
        "ScheduledActionSet": [
            {
                "ScheduledActionId": "asst-caa5ha40",
                "ScheduledActionName": "testv2-0",
                "AutoScalingGroupId": "asg-2nr9xh8h",
                "StartTime": "2018-09-28T00:00:00+08:00",
                "Recurrence": "0 0 * * *",
                "EndTime": "2018-09-28T23:59:59+08:00",
                "MaxSize": 10,
                "DesiredCapacity": 0,
                "MinSize": 0,
                "CreatedTime": "2018-09-24T07:41:54Z"
            }
        ]
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeScheduledActions)

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
| InvalidParameter.Conflict | Multiple parameters specified conflict and cannot co-exist. |
| InvalidParameterValue.Filter | Invalid filter. |

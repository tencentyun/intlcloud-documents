## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (DescribeScheduledActions) is used to query the details of one or more scheduled actions.

* You can query the details of scheduled actions based on information such as scheduled action ID, scheduled action name, or auto scaling group ID. For more information on filters, see `Filter`.
* If the parameter is empty, a number (same as the `Limit`. The default is 20) of scheduled actions will be returned.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeScheduledActions |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| ScheduledActionIds.N | No | Array of String | ID(s) of the scheduled action(s) to be queried, such as `asst-am691zxo`. A maximum of 100 instances are allowed for each request. You cannot specify both ScheduledActionIds and Filters. |
| Filters.N | No | Array of [Filter](https://cloud.tencent.com/document/api/377/20453#Filter) | Filter condition. <br/><li> scheduled-action-id - String - Required: No - (Filter condition) Filter by scheduled action ID. </li><li> scheduled-action-name - String - Required: No - (Filter condition) Filter by scheduled action name. </li><li> auto-scaling-group-id - String - Required: No - (Filter condition) Filter by auto scaling group ID. </li> |
| Offset | No | Integer | Offset. Default is 0. For more information on Offset, see the relevant sections in API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| Limit | No | Integer | Number of returned results. It defaults to 20. The maximum is 100. For more information on Limit, see the relevant sections in API [Overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of scheduled actions that meet the condition |
| ScheduledActionSet | Array of [ScheduledAction](https://cloud.tencent.com/document/api/377/20453#ScheduledAction) | List of scheduled action details |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying a Scheduled Action

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

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeScheduledActions)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter.Conflict | The specified parameters conflict with each other and thus cannot be both specified |
| InvalidParameterValue.Filter | Invalid filter |

## 1. API Description

Domain name for API request: as.tencentcloudapi.com.

This API (DescribeScheduledActions) is used to query the details of one or more scheduled tasks.

* You can query the details of scheduled tasks according to its ID, name, or scaling group ID. For more information about filtering, see `Filter`.
* If the parameter is empty, a certain number (specified by Limit, which is 20 by default) of scheduled tasks are returned to the current user.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter `Region` is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the `Region` field, for example: as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeScheduledActions |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| ScheduledActionIds.N | No | Array of String | IDs of the scheduled tasks to be queried, such as `asst-am691zxo`. Up to 100 tasks are allowed for each request. You cannot specify both `ScheduledActionIds` and `Filters`. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter condition. <br/>* `scheduled-action-id` - String - Required: No - (Filter condition) Filter by scheduled task ID. <br/>* `scheduled-action-name` - String - Required: No - (Filter condition) Filter by scheduled task name. <br/>* `auto-scaling-group-id` - String - Required: No - (Filter condition) Filter by scaling group ID. |
| Offset | No | Integer | Offset. Default is 0. For more information on Offset, see the relevant sections in API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| Limit | No | Integer | Number of returned results. It defaults to 20. The maximum is 100. For more information on Limit, see the relevant sections in API [Overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of scheduled tasks that meet the condition |
| ScheduledActionSet | Array of [ScheduledAction](/document/api/377/20453#ScheduledAction) | List of scheduled task details |
| RequestId | String | Unique ID of the request, which is required for troubleshooting. |

## 4. Example

### Example 1 Query a scheduled task

#### Input example

```
https://as.tencentcloudapi.com/?Action=DescribeScheduledActions
&ScheduledActionIds.0=asst-caa5ha40
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "ScheduledActionSet": [
      {
        "AutoScalingGroupId": "asg-2nr9xh8h",
        "CreatedTime": "2018-09-24T07:41:54Z",
        "DesiredCapacity": 0,
        "EndTime": "2018-09-28T23:59:59+08:00",
        "MaxSize": 10,
        "MinSize": 0,
        "Recurrence": "0 0 * * *",
        "ScheduledActionId": "asst-caa5ha40",
        "ScheduledActionName": "testv2-0",
        "StartTime": "2018-09-28T00:00:00+08:00"
      }
    ],
    "TotalCount": 1
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeScheduledActions)

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
| InvalidParameter.Conflict | The specified parameters conflict with each other and thus cannot be both specified |
| InvalidParameterValue.Filter | Invalid filter |


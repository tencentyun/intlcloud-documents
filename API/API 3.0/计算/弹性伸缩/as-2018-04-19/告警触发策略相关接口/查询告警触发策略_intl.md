## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (DescribeScalingPolicies) is used to query alarm trigger policies.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeScalingPolicies |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingPolicyIds.N | No | Array of String | Query by one or more alarm policy IDs in the format of asp-i9vkg894. The maximum number of instances per request is 100. This parameter does not support specifying both `AutoScalingPolicyIds` and `Filters` at the same time. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter condition. <br/><li> auto-scaling-policy-id - String - Required: No - (Filter condition) Filter by alarm policy ID. </li><li> auto-scaling-group-id - String - Required: No - (Filter condition) Filter by auto scaling group ID. </li><li> scaling-policy-name - String - Required: No - (Filter condition) Filter by alarm policy name. </li><br/>The maximum number of `Filters` per request is 10, while that of `Filter.Values` is 5. This parameter does not support specifying both `AutoScalingPolicyIds` and `Filters` at the same time. |
| Limit | No | Integer | Number of returned results. The default value is 20. The maximum is 100. | For more information on `Limit`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| Offset | No | Integer | Offset. Default value: 0. For more information on `Offset`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| ScalingPolicySet | Array of [ScalingPolicy](/document/api/377/20453#ScalingPolicy) | List of AS alarm trigger policy details. |
| TotalCount | Integer | Number of eligible notifications. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying Alarm Trigger Policies

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeScalingPolicies
&AutoScalingPolicyIds.0=asp-5zffv598
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 1,
    "ScalingPolicySet": [
      {
        "AutoScalingGroupId": "asg-gbqa1n66",
        "AutoScalingPolicyId": "asp-5zffv598",
        "Cooldown": 100,
        "ScalingPolicyName": "cpu-test",
        "AdjustmentType": "CHANGE_IN_CAPACITY",
        "MetricAlarm": {
          "Period": 60,
          "ContinuousTime": 5,
          "ComparisonOperator": "GREATER_THAN_OR_EQUAL_TO",
          "Statistic": "AVERAGE",
          "Threshold": 60,
          "MetricName": "CPU_UTILIZATION"
        },
        "NotificationUserGroupIds": [],
        "AdjustmentValue": 10
      }
    ],
    "RequestId": "351dd0ef-27bc-4312-9287-48cd0835274b"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeScalingPolicies)

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
| InvalidFilter | Invalid filter. |
| InvalidParameter.Conflict | The specified parameters conflict with each other and thus cannot be both specified |
| LimitExceeded | Quota is exceeded. |

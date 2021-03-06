## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (CreateScalingPolicy) is used to create an alarm trigger policy.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreateScalingPolicy |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingGroupId | Yes | String | Auto scaling group ID |
| ScalingPolicyName | Yes | String | Name of the alarm trigger policy. |
| AdjustmentType | Yes | String | The method to adjust the desired number of instances after the alarm is triggered. Value range: <br><li>CHANGE_IN_CAPACITY: Increase or decrease the desired number of instances </li><li>EXACT_CAPACITY: Adjust to the specified desired number of instances </li> <li>PERCENT_CHANGE_IN_CAPACITY: Adjust the desired number of instances by percentage </li> |
| AdjustmentValue | Yes | Integer | The adjusted value of desired number of instances after the alarm is triggered. Value range: <br><li>When `AdjustmentType` is CHANGE_IN_CAPACITY, if `AdjustmentValue` is a positive value, some new instances will be added after the alarm is triggered, and if it is a negative value, some existing instances will be removed after the alarm is triggered </li> <li> When `AdjustmentType` is EXACT_CAPACITY, the value of `AdjustmentValue` is the desired number of instances after the alarm is triggered, which should be equal to or greater than 0 </li> <li> When `AdjustmentType` is PERCENT_CHANGE_IN_CAPACITY, if `AdjusmentValue` (in %) is a positive value, new instances will be added by percentage after the alarm is triggered; if it is a negative value, existing instances will be removed by percentage after the alarm is triggered. |
| MetricAlarm | Yes | [MetricAlarm](https://cloud.tencent.com/document/api/377/20453#MetricAlarm) | Alarm monitoring metric. |
| Cooldown | No | Integer | Cooldown period in seconds. Default value: 300 seconds. |
| NotificationUserGroupIds.N | No | Array of String | Notification group ID, which is the set of user group IDs and can be queried through the [DescribeUserGroup API](https://cloud.tencent.com/document/api/378/4404). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AutoScalingPolicyId | String | Alarm trigger policy ID. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Increasing the Desired Number of Instances by 1 If the Average CPU Utilization Is over 50% Within 1 Minute for 5 Consecutive Occurrences

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateScalingPolicy
&AutoScalingGroupId=asg-12wjuh0s
&ScalingPolicyName=cpu_policy_test
&AdjustmentType= CHANGE_IN_CAPACITY
&AdjustmentValue=1
&Cooldown=60
&MetricAlarm.ComparisonOperator=GREATER_THAN
&MetricAlarm.MetricName=CPU_UTILIZATION
&MetricAlarm.Statistic=AVERAGE
&MetricAlarm.Threshold=50
&MetricAlarm.Period=60
&MetricAlarm.ContinuousTime=5
&NotificationUserGroupIds.0=1678
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "AutoScalingPolicyId": "asp-iir70sxv",
    "RequestId": "fb02c8bd-5f38-4786-91b6-0c6e06a88832"
  }
}
```

### Sample 2. Removing 50% Instances If the Average Memory Utilization Is Below 35% Within 1 Minute for 5 Consecutive Occurrences

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreateScalingPolicy
&AutoScalingGroupId=asg-12wjuh0s
&ScalingPolicyName=mem_policy_test
&AdjustmentType= PERCENT_CHANGE_IN_CAPACITY
&AdjustmentValue=-50
&Cooldown=300
&MetricAlarm.ComparisonOperator=LESS_THAN
&MetricAlarm.MetricName=MEM_UTILIZATION
&MetricAlarm.Statistic=AVERAGE
&MetricAlarm.Threshold=50
&MetricAlarm.Period=60
&MetricAlarm.ContinuousTime=5
&NotificationUserGroupIds.0=1678
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "AutoScalingPolicyId": "asp-f59pppuh",
    "RequestId": "116213d6-2269-44cc-af76-c4a8dc7dbdf9"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreateScalingPolicy)

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
| InvalidParameterValue.LimitExceeded | The value exceeds the limit. |
| InvalidParameterValue.ScalingPolicyNameDuplicate | The alarm policy name already exists. |
| InvalidParameterValue.UserGroupIdNotFound | The user group does not exist. |
| ResourceNotFound.AutoScalingGroupIdNotFound | The auto scaling group does not exist |

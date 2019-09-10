## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (DescribeAutoScalingActivities) is used to query activity history of an auto scaling group.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter Region is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in Region, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeAutoScalingActivities |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| ActivityIds.N | No | Array of String | Query by one or more scaling activity IDs in the format of `asa-5l2ejpfo`. The maximum quantity per request is 100. This parameter does not support specifying both `ActivityIds` and `Filters` at the same time. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter. <br/><li> auto-scaling-group-id - String - Required: No - (Filter) Filter by auto scaling group ID. </li><li> activity-status-code - String - Required: No - (Filter) Filter by scaling activity status. (INIT: initializing &#124; RUNNING: running &#124; SUCCESSFUL: succeeded &#124; PARTIALLY_SUCCESSFUL: partially succeeded &#124; FAILED: failed &#124; CANCELLED: canceled) </li><li> activity-type - String - Required: No - (Filter) Filter by scaling activity type. (SCALE_OUT: scale-out &#124; SCALE_IN: scale-in &#124; ATTACH_INSTANCES: adding an instance &#124; REMOVE_INSTANCES: terminating an instance &#124; DETACH_INSTANCES: removing an instance &#124; TERMINATE_INSTANCES_UNEXPECTEDLY: terminating an instance in the CVM Console &#124; REPLACE_UNHEALTHY_INSTANCE: replacing an unhealthy instance &#124; UPDATE_LOAD_BALANCERS: updating a load balancer) </li><li> activity-id - String - Required: No - (Filter) Filter by scaling activity ID. </li><br/>The maximum number of `Filters` per request is 10, while that of `Filter.Values` is 5. This parameter does not support specifying both `ActivityIds` and `Filters` at the same time. |
| Limit | No | Integer | Number of returned results. It defaults to 20. The maximum is 100. | For more information on `Limit`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| Offset | No | Integer | Offset. Default value: 0. For more information on `Offset`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| StartTime | No | Timestamp | The earliest start time of the scaling activity, which will be ignored if ActivityIds is specified. The value is in `UTC time` in the format of `YYYY-MM-DDThh:mm:ssZ` according to the `ISO8601` standard. |
| EndTime | No | Timestamp | The latest end time of the scaling activity, which will be ignored if ActivityIds is specified. The value is in `UTC time` in the format of `YYYY-MM-DDThh:mm:ssZ` according to the `ISO8601` standard. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of eligible scaling activities. |
| ActivitySet | Array of [Activity](/document/api/377/20453#Activity) | Information set of eligible scaling activities. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Using Filters to View the Scaling Activity List

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingActivities
&Filters.0.Name=activity-id
&Filters.0.Values.0=asa-o4v87ae9
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 1,
    "ActivitySet": [
      {
        "Description": "Activity was launched in response to a difference between desired capacity and actual capacity, scale out 1 instance(s).",
        "AutoScalingGroupId": "asg-2umy3jbd",
        "ActivityRelatedInstanceSet": [
          {
            "InstanceId": "ins-q3ss14yo",
            "InstanceStatus": "SUCCESSFUL"
          }
        ],
        "ActivityType": "SCALE_OUT",
        "ActivityId": "asa-o4v87ae9",
        "StartTime": "2018-11-20T08:33:56Z",
        "CreatedTime": "2018-11-20T08:33:56Z",
        "EndTime": "2018-11-20T08:34:52Z",
        "Cause": "Activity was launched in response to a difference between desired capacity and actual capacity.",
        "StatusMessageSimplified": "Success",
        "StatusMessage": "Success",
        "StatusCode": "SUCCESSFUL"
      }
    ],
    "RequestId": "1082ab5d-c985-4d8c-bb9d-0d05e282b4a7"
  }
}
```

### Sample 2. Querying Scaling Activity List by Scaling Activity ID

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingActivities
&ActivityIds.0=asa-o4v87ae9
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 1,
    "ActivitySet": [
      {
        "Description": "Activity was launched in response to a difference between desired capacity and actual capacity, scale out 1 instance(s).",
        "AutoScalingGroupId": "asg-2umy3jbd",
        "ActivityRelatedInstanceSet": [
          {
            "InstanceId": "ins-q3ss14yo",
            "InstanceStatus": "SUCCESSFUL"
          }
        ],
        "ActivityType": "SCALE_OUT",
        "ActivityId": "asa-o4v87ae9",
        "StartTime": "2018-11-20T08:33:56Z",
        "CreatedTime": "2018-11-20T08:33:56Z",
        "EndTime": "2018-11-20T08:34:52Z",
        "Cause": "Activity was launched in response to a difference between desired capacity and actual capacity.",
        "StatusMessageSimplified": "Success",
        "StatusMessage": "Success",
        "StatusCode": "SUCCESSFUL"
      }
    ],
    "RequestId": "1082ab5d-c985-4d8c-bb9d-0d05e282b4a7"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingActivities)

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
| InvalidParameter.Conflict | The specified parameters conflict with each other and thus cannot be both specified |
| InvalidParameterValue.Filter | Invalid filter |
| InvalidParameterValue.LimitExceeded | The value exceeds the limit. |

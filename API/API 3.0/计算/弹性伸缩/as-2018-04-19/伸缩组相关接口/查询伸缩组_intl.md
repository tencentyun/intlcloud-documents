## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (DescribeAutoScalingGroups) is used to query the information of auto scaling groups.

* You can query the details of auto scaling groups based on information such as auto scaling group ID, auto scaling group name, or launch configuration ID. For more information on filters, see `Filter`.
* If the parameter is empty, a number (same as the `Limit`. The default is 20) of auto scaling groups will be returned.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeAutoScalingGroups |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingGroupIds.N | No | Array of String | Query by one or more auto scaling group IDs in the format of `asg-nkdwoui0`. The maximum quantity per request is 100. This parameter does not support specifying both `AutoScalingGroupIds` and `Filters` at the same time. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter. <br/><li> auto-scaling-group-id - String - Required: No - (Filter) Filter by auto scaling group ID. </li><li> auto-scaling-group-name - String - Required: No - (Filter) Filter by auto scaling group name. </li><li> launch-configuration-id - String - Required: No - (Filter) Filter by launch configuration ID. </li><li> tag-key - String - Required: No - (Filter) Filter by tag key. </li><li> tag-value - String - Required: No - (Filter) Filter by tag value. </li><li> tag:tag-key - String - Required: No - (Filter) Filter by tag key-value pair. tag-key should be replaced with a specific tag key. For usage, see sample 2. </li><br/>The maximum number of `Filters` per request is 10, while that of `Filter.Values` is 5. This parameter does not support specifying both `AutoScalingGroupIds` and `Filters` at the same time. |
| Limit | No | Integer | Number of returned results. It defaults to 20. The maximum is 100. | For more information on `Limit`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| Offset | No | Integer | Offset. Default value: 0. For more information on `Offset`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AutoScalingGroupSet | Array of [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup) | List of auto scaling group details |
| TotalCount | Integer | Number of auto scaling groups that meet the condition |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying an Auto Scaling Group

The sample code below shows how to query an auto scaling group by ID.

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingGroups
&AutoScalingGroupIds.0=asg-nkdwoui0
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "AutoScalingGroupSet": [
      {
        "LaunchConfigurationId": "asc-7vucy6ae",
        "ForwardLoadBalancerSet": [
          {
            "TargetAttributes": [
              {
                "Port": 8080,
                "Weight": 10
              }
            ],
            "LocationId": "loc-l3hmaev9",
            "ListenerId": "lbl-ncw704sn",
            "LoadBalancerId": "lb-23aejgcv"
          }
        ],
        "LoadBalancerIdSet": [],
        "InstanceCount": 1,
        "DesiredCapacity": 1,
        "AutoScalingGroupStatus": "NORMAL",
        "AutoScalingGroupId": "asg-nkdwoui0",
        "ProjectId": 0,
        "TerminationPolicySet": [
          "OLDEST_INSTANCE"
        ],
        "AutoScalingGroupName": "vpc-7layer-lb",
        "InActivityStatus": "NOT_IN_ACTIVITY",
        "InServiceInstanceCount": 1,
        "DefaultCooldown": 301,
        "MinSize": 0,
        "MaxSize": 10,
        "VpcId": "vpc-hy436tmc",
        "LaunchConfigurationName": "launch configuration 1",
        "CreatedTime": "2018-09-27T02:01:28Z",
        "SubnetIdSet": [
          "subnet-3tmerl37",
          "subnet-b0vxjhot"
        ],
        "EnabledStatus": "ENABLED",
        "ZoneSet": []
      }
    ],
    "TotalCount": 1,
    "RequestId": "b8d3660c-bed1-40ad-9e7d-77390c9610be"
  }
}
```

### Sample 2. Querying Auto Scaling Groups Bound to a Tag

Query the auto scaling groups bound to the tag key-value pair (city:shenzhen).

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingGroups
&Filters.0.Name=tag:city
&Filters.0.Values.0=shenzhen
&Offset=0
&Limit=1
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "AutoScalingGroupSet": [
      {
        "LaunchConfigurationId": "asc-7vucy6ae",
        "ForwardLoadBalancerSet": [
          {
            "TargetAttributes": [
              {
                "Port": 8080,
                "Weight": 10
              }
            ],
            "LocationId": "loc-l3hmaev9",
            "ListenerId": "lbl-ncw704sn",
            "LoadBalancerId": "lb-23aejgcv"
          }
        ],
        "LoadBalancerIdSet": [],
        "InstanceCount": 1,
        "DesiredCapacity": 1,
        "AutoScalingGroupStatus": "NORMAL",
        "AutoScalingGroupId": "asg-nkdwoui0",
        "ProjectId": 0,
        "TerminationPolicySet": [
          "OLDEST_INSTANCE"
        ],
        "AutoScalingGroupName": "vpc-7layer-lb",
        "InActivityStatus": "NOT_IN_ACTIVITY",
        "InServiceInstanceCount": 1,
        "DefaultCooldown": 301,
        "MinSize": 0,
        "MaxSize": 10,
        "VpcId": "vpc-hy436tmc",
        "LaunchConfigurationName": "launch configuration 1",
        "CreatedTime": "2018-09-27T02:01:28Z",
        "SubnetIdSet": [
          "subnet-3tmerl37",
          "subnet-b0vxjhot"
        ],
        "EnabledStatus": "ENABLED",
        "ZoneSet": [],
        "Tags": [
          {
            "Key": "city",
            "Value": "shenzhen"
          }
        ]
      }
    ],
    "TotalCount": 1,
    "RequestId": "b8d3660c-bed1-40ad-9e7d-77390c9610be"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingGroups)

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
| InvalidParameterConflict | The two parameters conflict with each other, and cannot be both specified. |
| InvalidParameterValue.Filter | Invalid filter |
| InvalidPermission | The account does not support this operation. |

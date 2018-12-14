## 1. API Description

Domain name for API request: as.tencentcloudapi.com.

This API (DescribeAutoScalingGroups) is used to query the information of one or more scaling groups.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter `Region` is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​ used for this API: DescribeAutoScalingGroups |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingGroupIds.N | No | Array of String | IDs of the scaling groups to be queried, such as `asg-nkdwoui0`. Up to 100 scaling groups can be queried at one time. You cannot specify both `AutoScalingGroups` and `Filters`. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter condition. <br/><li> `auto-scaling-group-id` - String - Required: No - (Filter condition) Filter by scaling group ID. </li><li> `auto-scaling-group-name` - String - Required: No - (Filter condition) Filter by scaling group name. </li><li> `launch-configuration-id` - String - Required: No - (Filter condition) Filter by launch configuration ID. </li><br/> You can specify 10 `Filters` and 5 `Filter.Values` in one request. You cannot specify both `AutoScalingGroupIds` and `Filters`. |
| Limit | No | Integer | Number of returned results. It defaults to 20. The maximum is 100. For more information on `Limit`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| Offset | No | Integer | Offset. It is 0 by default. For more information on `Offset`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AutoScalingGroupSet | Array of [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup) | List of scaling group details |
| TotalCount | Integer | Number of scaling groups that meet the condition |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the information of a scaling group

#### Input example

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingGroups
&AutoScalingGroupIds.0=asg-nkdwoui0
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "AutoScalingGroupSet": [
      {
        "AutoScalingGroupId": "asg-nkdwoui0",
        "AutoScalingGroupName": "vpc-7layer-lb",
        "AutoScalingGroupStatus": "NORMAL",
        "CreatedTime": "2018-09-27T02:01:28Z",
        "DefaultCooldown": 301,
        "DesiredCapacity": 1,
        "EnabledStatus": "ENABLED",
        "ForwardLoadBalancerSet": [
          {
            "ListenerId": "lbl-ncw704sn",
            "LoadBalancerId": "lb-23aejgcv",
            "LocationId": "loc-l3hmaev9",
            "TargetAttributes": [
              {
                "Port": 8080,
                "Weight": 10
              }
            ]
          }
        ],
        "InServiceInstanceCount": 1,
        "InstanceCount": 1,
        "LaunchConfigurationId": "asc-7vucy6ae",
        "LaunchConfigurationName": "Launch configuration 1",
        "LoadBalancerIdSet": [],
        "MaxSize": 10,
        "MinSize": 0,
        "ProjectId": 0,
        "SubnetIdSet": [
          "subnet-3tmerl37",
          "subnet-b0vxjhot"
        ],
        "TerminationPolicySet": [
          "OLDEST_INSTANCE"
        ],
        "VpcId": "vpc-hy436tmc",
        "ZoneSet": []
      }
    ],
    "RequestId": "b8d3660c-bed1-40ad-9e7d-77390c9610be",
    "TotalCount": 1
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingGroups)

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
| InvalidFilter | Invalid filter |
| InvalidParameterConflict | The two parameters conflict with each other, and cannot be both specified. |
| InvalidParameterValue.Filter | Invalid filter |
| InvalidPermission | This operation is not supported for the account |


## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (DescribeAutoScalingGroups) describes one or more scaling groups.

* You can query the details of scaling groups based on information such as scaling group ID, scaling group name, or launch configuration ID. For more information about filters, see `Filter`.
* If the parameter is empty, a number (same as the `Limit`. The default is 20) of scheduled tasks will be returned.

Default API request frequency limit: 20 times/second.

Note: Because financial availability zones and non-financial availability zones are isolated. When specifying a financial availability zone (e.g., ap-shanghai-fsi) in the Region (a common parameter), you should also choose the financial availability zone preferably in the same region as that one specified in Region for the domain, such as as.ap-shanghai-fsi.tencentcloudapi.com.


## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/377/20426).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeAutoScalingGroups |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
|  AutoScalingGroupIds.N | No | Array of String | Query by one or more scaling group IDs. Scaling group ID example: `asg-nkdwoui0`. The upper limit per request is 100. The parameter does not support specifying both `AutoScalingGroups` and `Filters` at the same time. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter. <br/><li> auto-scaling-group-id - String - Required: No - (Filter) Filter by scaling group ID. </li><li> auto-scaling-group-name - String - Required: No - (Filter) Filter by scaling group name. </li><li> launch-configuration-id - String - Required: No - (Filter) Filter by launch configuration ID. </li><br/>The maximum number of `Filters` per request is 10. The upper limit for `Filter.Values` is 5. The parameter does not support specifying both `AutoScalingGroupIds` and `Filters` at the same time. |
| Limit | No | Integer | Number of returned results, 20 by default, up to 100. For more information about `Limit`, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |
| Offset | No | Integer | Offset, 0 by default. For more information about `Offset`, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| AutoScalingGroupSet | Array of [AutoScalingGroup](/document/api/377/20453#AutoScalingGroup) | List of scaling group details. |
| TotalCount | Integer | Number of eligible scaling groups. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues |

## 4. Sample

### Querying a Scaling Group

This is to query a scaling group by the specified scaling group ID.

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


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingGroups)

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

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidFilter | Invalid filter. |
| InvalidParameterConflict | Parameters that cannot co-exist were specified. |
| InvalidParameterValue.Filter | Invalid filter. |
| InvalidPermission | The account does not support this operation. |

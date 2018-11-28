## 1. API Description

Domain name for API request: as.tencentcloudapi.com.

This API (DescribeAutoScalingInstances) is used to query the information of auto scaling instances.



Default request rate limit: 10/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter `Region` is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value ​used for this API: DescribeAutoScalingInstances |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceIds.N | No | Array of String | IDs of CVM instances to be queried. You cannot specify both InstanceIds and Filters. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter condition. <br/><li> instance-id - String - Required: No - (Filter condition) Filter by instance ID. </li><li> auto-scaling-group-id - String - Required: No - (Filter condition) Filter by scaling group ID. </li><br/> You can specify 10 `Filters` and 5 `Filter.Values` in one request. You cannot specify both `InstanceIds` and `Filters`. |
| Offset | No | Integer | Offset. It is 0 by default. For more information on `Offset`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| Limit | No | Integer | Number of returned results. It defaults to 20. The maximum is 100. For more information on `Limit`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AutoScalingInstanceSet | Array of [Instance](/document/api/377/20453#Instance) | Instance details list |
| TotalCount | Integer | Number of instances that meet the condition |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query a specified instance

#### Input example

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingInstances
&InstanceIds.0=ins-1fswxz1m
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "AutoScalingInstanceSet": [
      {
        "AddTime": "2018-08-21T12:05:12Z",
        "AutoScalingGroupId": "asg-4o61gsxi",
        "CreationType": "AUTO_CREATION",
        "HealthStatus": "HEALTHY",
        "InstanceId": "ins-1fswxz1m",
        "LaunchConfigurationId": "asc-5fzsm72a",
        "LaunchConfigurationName": "Series 2 local disk",
        "LifeCycleState": "IN_SERVICE",
        "ProtectedFromScaleIn": false,
        "Zone": "ap-guangzhou-3"
      }
    ],
    "RequestId": "2ae3e836-d47a-431c-b54b-4e1c2f419e5b",
    "TotalCount": 1
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingInstances)

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
| InvalidFilter | Invalid filter |
| InvalidParameter.Conflict | The specified parameters conflict with each other and thus cannot be both specified |
| InvalidParameterValue.Filter | Invalid filter |


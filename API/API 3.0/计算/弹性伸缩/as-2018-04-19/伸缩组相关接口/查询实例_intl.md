## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (DescribeAutoScalingInstances) is used to query information about the instances associated with Auto Scaling.

* You can query the details of instances based on information such as instance ID and scaling group ID. For more information about filters, see `Filter`.
* If the parameter is empty, a certain number of instances (specified by `Limit` and 20 by default) of the current user is returned.

Default API request frequency limit: 10 times/second.

Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/377/20426).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeAutoScalingInstances |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| InstanceIds.N | No | Array of String | ID of the CVM instance to be queried. The parameter does not support specifying both InstanceIds and Filters at the same time. |
| Filters.N | No | Array of [Filter](/document/api/377/20453#Filter) | Filter. <br/><li> instance-id - String - Required: No - (Filter) Filter by instance ID. </li><li> auto-scaling-group-id - String - Required: No - (Filter) Filter by scaling group ID. </li><br/>The maximum number of `Filters` per request is 10. The upper limit for `Filter.Values` is 5. The parameter does not support specifying both `InstanceIds` and `Filters` at the same time. |
| Offset | No | Integer | Offset, 0 by default. For more information about `Offset`, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |
| Limit | No | Integer | Number of returned results, 20 by default, up to 100. For more information about `Limit`, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| AutoScalingInstanceSet | Array of [Instance](/document/api/377/20453#Instance) | List of instance details. |
| TotalCount | Integer | Number of eligible instances. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Querying a Specified Instance

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingInstances
&InstanceIds.0=ins-1fswxz1m
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "TotalCount": 1,
        "AutoScalingInstanceSet": [
            {
                "ProtectedFromScaleIn": false,
                "Zone": "ap-guangzhou-3",
                "LaunchConfigurationId": "asc-5fzsm72a",
                "InstanceId": "ins-1fswxz1m",
                "AddTime": "2018-08-21T12:05:12Z",
                "CreationType": "AUTO_CREATION",
                "AutoScalingGroupId": "asg-4o61gsxi",
                "HealthStatus": "HEALTHY",
                "LifeCycleState": "IN_SERVICE",
                "LaunchConfigurationName": "series 2 local disk",
                "InstanceType": "S2.SMALL2"
            }
        ],
        "RequestId": "2ae3e836-d47a-431c-b54b-4e1c2f419e5b"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingInstances)

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
| InvalidFilter | Invalid filter. |
| InvalidParameter.Conflict | Multiple parameters specified conflict and cannot co-exist. |
| InvalidParameterValue.Filter | Invalid filter. |

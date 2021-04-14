## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (DescribeAutoScalingInstances) is used to query information on the instances with AS.

* You can query the details of instances based on information such as instance ID and auto scaling group ID. For more information on filters, see `Filter`.
* If the parameter is empty, a number (same as the `Limit`. The default is 20) of instances will be returned.

Default API request rate limit: 10 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeAutoScalingInstances |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceIds.N | No | Array of String | ID of the CVM instance to be queried. This parameter does not support specifying both InstanceIds and Filters at the same time. |
| Filters.N | No | Array of [Filter](https://cloud.tencent.com/document/api/377/20453#Filter) | Filter. <br/><li> instance-id - String - Required: No - (Filter) Filter by instance ID. </li><li> auto-scaling-group-id - String - Required: No - (Filter) Filter by auto scaling group ID. </li><br/>The maximum number of `Filters` per request is 10, while that of `Filter.Values` is 5. This parameter does not support specifying both `InstanceIds` and `Filters` at the same time. |
| Offset | No | Integer | Offset. Default value: 0. For more information on `Offset`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |
| Limit | No | Integer | Number of returned results. It defaults to 20. The maximum is 100. | For more information on `Limit`, see relevant section in the API [Overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AutoScalingInstanceSet | Array of [Instance](https://cloud.tencent.com/document/api/377/20453#Instance) | Instance details list |
| TotalCount | Integer | Number of instances that meet the condition |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying a Specified Instance

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
        "VersionNumber": 1,
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

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingInstances)

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
| InvalidFilter | Invalid filter. |
| InvalidParameter.Conflict | The specified parameters conflict with each other and thus cannot be both specified |
| InvalidParameterValue.Filter | Invalid filter |

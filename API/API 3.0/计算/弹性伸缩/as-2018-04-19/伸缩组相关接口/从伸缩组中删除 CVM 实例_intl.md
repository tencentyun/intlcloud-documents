## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (RemoveInstances) is used to delete CVM instances from an auto scaling group. Instances created automatically by AS will be terminated, while those created and added to the auto scaling group will be removed and retained.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: RemoveInstances |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoScalingGroupId | Yes | String | Auto scaling group ID |
| InstanceIds.N | Yes | Array of String | List of CVM instance IDs |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| ActivityId | String | Scaling activity ID |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Removing an Instance from an Auto Scaling Group

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=RemoveInstances
&AutoScalingGroupId=asg-boz1qhnk
&InstanceIds.0=ins-cri8d02t
&InstanceIds.1=ins-osckfnm7
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "ActivityId": "asa-dne04cxp",
    "RequestId": "5b039ee6-e8ff-4605-bb24-b45337747431"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=RemoveInstances)

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
| InvalidParameterValue.LimitExceeded | The value exceeds the limit. |
| ResourceInsufficient.AutoScalingGroupBelowMinSize | The number of instances in the auto scaling group is below the minimum value. |
| ResourceNotFound.AutoScalingGroupIdNotFound | The auto scaling group does not exist |
| ResourceNotFound.InstancesNotInAutoScalingGroup | The target instance is not in the auto scaling group. |
| ResourceUnavailable.AutoScalingGroupInActivity | The auto scaling group is active. |

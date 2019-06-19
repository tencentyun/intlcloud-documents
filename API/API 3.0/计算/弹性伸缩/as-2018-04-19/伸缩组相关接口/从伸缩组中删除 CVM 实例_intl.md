## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (RemoveInstances) is used to remove a CVM instance from a scaling group. According to the current product logic, if the instance is automatically created by Auto Scaling, it will be terminated; if it is added to the scaling group after creation, it will be removed from the scaling group but not terminated.

Default API request frequency limit: 20 times/second.

Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/377/20426).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: RemoveInstances |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| AutoScalingGroupId | Yes | String | Scaling group ID |
| InstanceIds.N | Yes | Array of String | List of CVM instance IDs |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting |

## 4. Sample

### Removing an Instance from a Scaling Group

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
        "RequestId": "5b039ee6-e8ff-4605-bb24-b45337747431"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=RemoveInstances)

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
| InvalidParameterValue.LimitExceeded | The value exceeds the limit. |
| ResourceInsufficient.AutoScalingGroupBelowMinSize | The number of instances in the scaling group is below the minimum value. |
| ResourceNotFound.AutoScalingGroupIdNotFound | The scaling group does not exist. |
| ResourceNotFound.InstancesNotInAutoScalingGroup | The target instance is not in the scaling group. |
| ResourceUnavailable.AutoScalingGroupInActivity | The scaling group is active. |

## 1. API Description

API domain name: emr.tencentcloudapi.com.

This API inquires about the price of creating an instance

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/589/33974).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: InquiryPriceCreateInstance |
| Version | Yes | String | Common parameter. The version of this API: 2019-01-03 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/589/33974#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| TimeUnit | Yes | String | Time unit |
| TimeSpan | Yes | Integer | Time span |
| ResourceSpec | Yes | [ResourceSpec](/document/api/589/33981#ResourceSpec) | Description of the inquired resource |
| Currency | Yes | String | Currency |
| PayMode | Yes | Integer | Billing method |
| SupportHA | Yes | Integer | Whether HA is supported. 1: yes; 0: no |
| Software.N | Yes | Array of String | Software list |
| Placement | Yes | [Placement](/document/api/589/33981#Placement) | Location information |
| VPCSettings | Yes | [VPCSettings](/document/api/589/33981#VPCSettings) | VPC information |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Result | [InquiryPriceResult](/document/api/589/33981#InquiryPriceResult) | Price inquiry result |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1. Inquiring About the Price of Creating an Instance

#### Input Sample Code

```
https://emr.tencentcloudapi.com/?Action=InquiryPriceCreateInstance
&Region=ap-beijing
&TimeUnit=m
&TimeSpan=1
&Placement.Zone=ap-chongqing-1
&Currency=CNY
&PayMode=1
&SupportHA=0
&Software.0=hadoop-2.7.3
&Software.1=zookeeper-3.4.9
&ResourceSpec.MasterResourceSpec.Memory=8192
&ResourceSpec.MasterResourceSpec.CPUCores=4
&ResourceSpec.MasterResourceSpec.Volume=100
&ResourceSpec.MasterResourceSpec.DiskType=CLOUD_PREMIUM
&ResourceSpec.MasterResourceSpec.Spec=CVM.S3
&ResourceSpec.MasterResourceSpec.RootDiskVolume=100
&ResourceSpec.MasterResourceSpec.StorageType=5
&ResourceSpec.CoreResourceSpec.Memory=8192
&ResourceSpec.CoreResourceSpec.CPUCores=4
&ResourceSpec.CoreResourceSpec.Volume=100
&ResourceSpec.CoreResourceSpec.DiskType=CLOUD_PREMIUM
&ResourceSpec.CoreResourceSpec.Spec=CVM.S3
&ResourceSpec.CoreResourceSpec.RootDiskVolume=100
&ResourceSpec.CoreResourceSpec.StorageType=5
&ResourceSpec.MasterCount=1
&ResourceSpec.CoreCount=2
&VPCSettings.VpcId=vpc-5p4i6ned
&VPCSettings.SubnetId=subnet-r19p3f8k
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Result": {
      "OriginalCost": 1557.99,
      "DiscountCost": 1049.44,
      "TimeUnit": "m",
      "TimeSpan": 1
    },
    "RequestId": "df9bfbd5-f182-446c-8827-56bff931e343"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=emr&Version=2019-01-03&Action=InquiryPriceCreateInstance)

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

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/589/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation | Operation failed. |
| InvalidParameter | Incorrect parameter. |
| InvalidParameterValue | Invalid parameter value. |
| MissingParameter | A parameter is missing. |
| UnknownParameter | Unknown parameter. |
| UnsupportedOperation | Unsupported operation. |

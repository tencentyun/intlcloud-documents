## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (CreatePaiInstance) is used to create a PAI instance.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CreatePaiInstance |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| DomainName | Yes | String | PAI instance domain name. |
| InternetAccessible | Yes | [InternetAccessible](/document/api/377/20453#InternetAccessible) | Information of the public network bandwidth configuration. |
| InitScript | No | String | The Base64-encoded string of the launch script. |
| Zones.N | No | Array of String | Availability zone list. |
| VpcId | No | String | VpcId. |
| SubnetIds.N | No | Array of String | List of subnets. |
| InstanceName | No | String | Instance display name. |
| InstanceTypes.N | No | Array of String | List of instance models. |
| LoginSettings | No | [LoginSettings](/document/api/377/20453#LoginSettings) | Instance login settings. |
| InstanceChargeType | No | String | Instance billing mode. |
| InstanceChargePrepaid | No | [InstanceChargePrepaid](/document/api/377/20453#InstanceChargePrepaid) | The relevant parameter setting for monthly subscription mode. This parameter can specify the purchased period, whether to set auto-renewal and other attributes of the instance purchased on a monthly subscription basis. This parameter is required if the billing mode for the specified instance is monthly subscription. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| InstanceIdSet | Array of String | This parameter is returned when an instance is created via this API, representing one or more instance `IDs`. The return of the instance `ID` list does not mean that the instances are created successfully. You can find out whether the instances are created by checking the status of the instance `IDs` in the InstancesSet returned by the [DescribeInstances API](https://cloud.tencent.com/document/api/213/15728). If the status of the instances changes from "preparing" to "running", the instances are created successfully. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Creating a PAI Instance

Create a PAI instance with specified parameters such as domain name

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CreatePaiInstance
&DomainName=apple-gz012345.pai.tcloudbase.com
&InitScript=IyEvYmluL2Jhc2gKZWNobyAiaGVsbG8iCg==
&Zones.0=ap-guangzhou-2
&InstanceChargeType=POSTPAID_BY_HOUR
&InstanceTypes.0=S4.SMALL2
&SystemDisk.DiskType=CLOUD_BASIC
&SystemDisk.DiskSize=50
&InternetAccessible.InternetChargeType=TRAFFIC_POSTPAID_BY_HOUR
&InternetAccessible.InternetMaxBandwidthOut=10
&InstanceName=PAI-TEST
&LoginSettings.Password=PAI@Test123
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "InstanceIdSet": [
      "ins-bmmk7d75"
    ],
    "RequestId": "843518b0-43bb-4066-a00b-d95b338b3142"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CreatePaiInstance)

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

This API has no error codes related to business logic. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

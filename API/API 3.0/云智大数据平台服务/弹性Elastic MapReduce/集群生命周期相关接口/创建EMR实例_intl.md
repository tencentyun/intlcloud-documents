## 1. API Description

API domain name: emr.tencentcloudapi.com.

This API creates an EMR instance.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/589/33974).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: CreateInstance |
| Version | Yes | String | Common parameter. The version of this API: 2019-01-03 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/589/33974#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| ProductId | Yes | Integer | Product ID |
| VPCSettings | Yes | [VPCSettings](/document/api/589/33981#VPCSettings) | VPC settings parameter |
| Software.N | Yes | Array of String | Software list |
| ResourceSpec | Yes | [ResourceSpec](/document/api/589/33981#ResourceSpec) | Resource description |
| SupportHA | Yes | Integer | Support for HA |
| InstanceName | Yes | String | Instance name |
| PayMode | Yes | Integer | Billing method |
| Placement | Yes | [Placement](/document/api/589/33981#Placement) | Cluster location information |
| TimeSpan | Yes | Integer | Time span |
| TimeUnit | Yes | String | Time unit |
| LoginSettings | Yes | [LoginSettings](/document/api/589/33981#LoginSettings) | Login configuration |
| ClientToken | Yes | String | Client token |
| COSSettings | No | [COSSettings](/document/api/589/33981#COSSettings) | COS settings parameter |
| SgId | No | String | Security group ID |
| PreExecutedFileSettings | No | [PreExecuteFileSettings](/document/api/589/33981#PreExecuteFileSettings) | Pre-execution script settings |
| AutoRenew | No | Integer | Auto-renewal |
| NeedMasterWan | No | String | Whether a public IP is needed. If yes, enter NEED_MASTER_WAN; if no, enter NOT_NEED_MASTER_WAN. NEED_MASTER_WAN by default |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Result | [CreateInstanceResult](/document/api/589/33981#CreateInstanceResult) | Instance creation result |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1 Create an instance

#### Input Sample Code

```
https://emr.tencentcloudapi.com/?Action=CreateInstance
&ProductId=2
&SupportHA=0
&InstanceName=jaco2
&PayMode=1
&Placement.Zone=ap-chongqing-1
&Placement.ProjectId=0
&AutoRenew=0
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
&LoginSettings.Password=emr%40cloud
&ClientToken=jaco1
&TimeSpan=1
&TimeUnit=m
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Result": {
      "ClientToken": "jaco1",
      "InstanceName": "jaco2",
      "DealNames": [
        "20190314261409",
        "20190314261410",
        "20190314261411",
        "20190314261412",
        "20190314261413",
        "20190314261414"
      ]
    },
    "RequestId": "701453be-7257-40e6-b5fd-4bbb01baae36"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=emr&Version=2019-01-03&Action=CreateInstance)

### SDK

TencentCloud API 3.0 integrates software development kits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see (/document/api/589/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |

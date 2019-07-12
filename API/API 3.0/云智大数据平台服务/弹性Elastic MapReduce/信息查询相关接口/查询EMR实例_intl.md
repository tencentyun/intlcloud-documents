## 1. API Description

API domain name: emr.tencentcloudapi.com.

This API describes one or more specified EMR instances.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/589/33974).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeInstances |
| Version | Yes | String | Common parameter. The version of this API: 2019-01-03 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/589/33974#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceIds.N | No | Array of String | Query the list. If this is left empty, the list of all instances under the AppId is returned |
| Offset | No | Integer | Query offset; 0 by default |
| Limit | No | Integer | Limit for query results. The default value is 10. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Result | [ClusterInfoResult](/document/api/589/33981#ClusterInfoResult) | Number of instances |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1. Querying Instance Details

#### Input Sample Code

```
https://emr.tencentcloudapi.com/?Action=DescribeInstances
&Offset=0
&Limit=1
&InstanceIds.0=emr-b3zor8nr
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Result": {
      "TotalCnt": 1,
      "ClusterList": [
        {
          "ClusterId": "emr-b3zor8nr",
          "StatusDesc": "Cluster running",
          "ClusterName": "jaco2",
          "ZoneId": 190001,
          "AppId": 1258469122,
          "Addtime": "2019-03-14 20:44:31",
          "Runtime": "0 days 3 hours 41 minutes 13 seconds",
          "Config": {
            "SoftInfo": [
              "zookeeper-3.4.9",
              "hadoop-2.7.3",
              "sys-1.0"
            ],
            "MasterNodeSize": 1,
            "CoreNodeSize": 2,
            "TaskNodeSize": 1,
            "ComNodeSize": 0,
            "MasterResourceSpec": {
              "CPUCores": 4,
              "DiskType": "CLOUD_PREMIUM",
              "Memory": 8192,
              "RootDiskVolume": 100,
              "Spec": "CVM.S3",
              "StorageType": 5,
              "Volume": 100,
              "SpecName": ""
            },
            "CoreResourceSpec": {
              "CPUCores": 4,
              "DiskType": "CLOUD_PREMIUM",
              "Memory": 8192,
              "RootDiskVolume": 100,
              "Spec": "CVM.S3",
              "StorageType": 5,
              "Volume": 100,
              "SpecName": ""
            },
            "TaskResourceSpec": {
              "CPUCores": 4,
              "DiskType": "CLOUD_PREMIUM",
              "Memory": 8192,
              "RootDiskVolume": 100,
              "Spec": "CVM.S3",
              "StorageType": 5,
              "Volume": 100,
              "SpecName": ""
            },
            "CommonResourceSpec": {
              "CPUCores": 0,
              "DiskType": "",
              "Memory": 0,
              "RootDiskVolume": 0,
              "Spec": "",
              "StorageType": 0,
              "Volume": 0,
              "SpecName": ""
            },
            "Oncos": false,
            "COSSettings": {
              "LogOnCosPath": "",
              "CosSecretId": "",
              "CosSecretKey": ""
            }
          },
          "MasterIp": "118.24.246.22",
          "EmrVersion": "EMR-V2.0.1",
          "ChargeType": 1
        }
      ]
    },
    "RequestId": "e83dffa2-34be-4069-bb35-5a62f11e6d45"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=emr&Version=2019-01-03&Action=DescribeInstances)

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
| InternalError.Test | The selected spec is sold out. |

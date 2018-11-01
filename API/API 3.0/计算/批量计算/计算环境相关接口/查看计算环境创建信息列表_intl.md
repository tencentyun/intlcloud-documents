## **1. API Description**
API request domain name: batch.tencentcloudapi.com.

This API is used to view the list of information about compute environment creation, including name, description, type, environment parameters, notifications and number of desired nodes.

Default API request frequency limit: 20 times/second.



## **2. Input Parameters**

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/599/15883).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeComputeEnvCreateInfos |
| Version | Yes | String | Common parameter; the value for this API: 2017-03-12 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/599/15883#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| EnvIds.N | No | Array of String | Compute environment ID |
| Filters.N | No | Array of [Filter](/document/api/599/15912#Filter) | Filter <br/><li> zone - String - Required: No - (Filter ) by availability zone. </li><li> env-id - String - Required: No - (Filter) by compute environment ID. </li><li> env-name - String - Required: No - (Filter) by compute environment name. </li> |
| Offset | No | Integer | Offset |
| Limit | No | Integer | Max number of entries returned |

## **3. Output Parameters**

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of compute environments |
| ComputeEnvCreateInfoSet | Array of [ComputeEnvCreateInfo](/document/api/599/15912#ComputeEnvCreateInfo) | List of compute environment creation information |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing List of Compute Environment Creation Information

#### Input

```
https://batch.tencentcloudapi.com/?Action=DescribeComputeEnvCreateInfos
&EnvIds.0=env-lcx7qbbr
&Filters.1.Name=env-id
&Filters.1.Values.1=env-lcpcej85
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "ComputeEnvCreateInfoSet": [
      {
        "DesiredComputeNodeCount": 1,
        "EnvData": {
          "ImageId": "img-8toqc6s3",
          "InstanceType": "S3.4XLARGE32",
          "InternetAccessible": {
            "InternetMaxBandwidthOut": "50",
            "PublicIpAssigned": "TRUE"
          },
          "LoginSettings": {
            "Password": "B1[habcd"
          },
          "SystemDisk": {
            "DiskSize": "50",
            "DiskType": "CLOUD_BASIC"
          }
        },
        "EnvDescription": "batch env ",
        "EnvId": "env-lcx7qbbr",
        "EnvName": "batch-spot",
        "EnvType": "MANAGED"
      },
      {
        "DesiredComputeNodeCount": 1,
        "EnvData": {
          "ImageId": "img-8toqc6s3",
          "InstanceType": "S3.4XLARGE32",
          "InternetAccessible": {
            "InternetMaxBandwidthOut": "50",
            "PublicIpAssigned": "TRUE"
          },
          "LoginSettings": {
            "Password": "B1[habcd"
          },
          "SystemDisk": {
            "DiskSize": "50",
            "DiskType": "CLOUD_BASIC"
          }
        },
        "EnvDescription": "batch env ",
        "EnvId": "env-lcpcej85",
        "EnvName": "batch-spot",
        "EnvType": "MANAGED"
      }
    ],
    "RequestId": "c50bfbf1-d214-4e41-90f6-39270dc9f071",
    "TotalCount": 2
  }
}
```


## 5. Developer Resources

**It is recommended to use [`API 3.0 Explorer`](https://console.cloud.tencent.com/api/explorer). This tool provides various capabilities such as online debugging, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

Cloud API 3.0 comes with a set of complementary development tools that make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/599/15885#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter.EnvIdMalformed | Invalid compute environment ID format. |
| InvalidParameterValue | Invalid parameter value. |
| InvalidZone.MismatchRegion | The specified zone does not exist. |
| UnknownParameter | Unknown parameter error |


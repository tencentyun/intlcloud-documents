## **1. API Description**
API request domain name: batch.tencentcloudapi.com.

This API is used to view the compute environment creation information.

Default API request frequency limit: 2 times/second.



## **2. Input Parameters**

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/599/15883).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeComputeEnvCreateInfo |
| Version | Yes | String | Common parameter; the value for this API: 2017-03-12 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/599/15883#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| EnvId | Yes | String | Compute environment ID |

## **3. Output Parameters**

| Parameter name | Type | Description |
|---------|---------|---------|
| EnvId | String | Compute environment ID |
| EnvName | String | Compute environment name |
| EnvDescription | String | Compute environment description |
| EnvType | String | Compute environment type; only "MANAGED" type is supported |
| EnvData | [EnvData](/document/api/599/15912#EnvData) | Compute environment parameter |
| MountDataDisks | Array of [MountDataDisk](/document/api/599/15912#MountDataDisk) | Data disk mounting option |
| InputMappings | Array of [InputMapping](/document/api/599/15912#InputMapping) | Input mapping |
| Authentications | Array of [Authentication](/document/api/599/15912#Authentication) | Authentication information |
| Notifications | Array of [Notification](/document/api/599/15912#Notification) | Notification information |
| DesiredComputeNodeCount | Integer | Number of desired compute nodes |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Compute Environment Creation Information

#### Input

```
https://batch.tencentcloudapi.com/?Action=DescribeComputeEnvCreateInfo
&EnvId=env-lcpcej85
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "DesiredComputeNodeCount": 2,
    "EnvData": {
      "DataDisks": [
        {
          "DiskSize": 50,
          "DiskType": "CLOUD_BASIC"
        }
      ],
      "ImageId": "img-bd78fy2t",
      "InstanceType": "S1.SMALL2",
      "InternetAccessible": {
        "InternetMaxBandwidthOut": 50,
        "PublicIpAssigned": "TRUE"
      },
      "SystemDisk": {
        "DiskSize": 50,
        "DiskType": "CLOUD_BASIC"
      },
      "VirtualPrivateCloud": {
        "SubnetId": "subnet-8axej2jc",
        "VpcId": "vpc-cg18la4l"
      }
    },
    "EnvDescription": "test compute env",
    "EnvId": "env-qleawxzt",
    "EnvName": "test compute env",
    "EnvType": "MANAGED",
    "InputMappings": [
      {
        "DestinationPath": "/mnt/disk/",
        "SourcePath": "cos://bucket-appid.cos.ap-hongkong.myqcloud.com/"
      },
      {
        "DestinationPath": "/mnt/input/",
        "SourcePath": "cos://bucket-appid.cos.ap-hongkong.myqcloud.com/test/"
      }
    ],
    "Notifications": [
      {
        "EventConfigs": [
          {
            "EventName": "ComputeEnvCreated",
            "EventVars": [
              {
                "Name": "name1",
                "Value": "value1"
              },
              {
                "Name": "name2",
                "Value": "value2"
              }
            ]
          }
        ],
        "TopicName": "topic name"
      }
    ],
    "RequestId": "578f3fae-6908-4521-ac07-17c2cffcd5ae"
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

This API has no error codes related to business logic. For other error codes, see [Common Error Codes](/document/api/599/15885#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).


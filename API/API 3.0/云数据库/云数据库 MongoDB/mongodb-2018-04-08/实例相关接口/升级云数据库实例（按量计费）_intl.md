## 1. API Description

Domain name for API request: mongodb.tencentcloudapi.com.

This API (UpgradeDBInstanceHour) is used to upgrade a pay-as-you-go MongoDB database instance to expand memory, storage and Oplog capacity.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mongodb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/240/31800).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: UpgradeDBInstanceHour. |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-08 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/240/31800#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Instance ID, such as: cmgo-p8vnipr5. |
| Memory | Yes | Integer | The memory capacity to which the instance will be upgraded (in GB). |
| Volume | Yes | Integer | The disk capacity to which the instance will be upgraded (in GB). |
| OplogSize | No | Integer | The Oplog capacity to which the instance will be upgraded (in GB). It is 10% of the disk capacity by default. The minimum value allowed is 10% of disk capacity, and the maximum is 90% of disk capacity. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DealId | String | Order ID |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Upgrade a pay-as-you-go database instance

You need to upgrade a pay-as-you-go database instance using an API.

#### Input example

```
https://mongodb.tencentcloudapi.com/?Action=UpgradeDBInstanceHour
&Memory=4
&Volume=250
&InstanceId=cmgo-f555zzz
&OplogSize=25
&<Common request parameters>
```

#### Output example

```
{
    "Response":{
        "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7",
        "DealId":"20171201160000002670226599824833"
    }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mongodb&Version=2018-04-08&Action=UpgradeDBInstanceHour)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/240/31803#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameter | Invalid parameter |


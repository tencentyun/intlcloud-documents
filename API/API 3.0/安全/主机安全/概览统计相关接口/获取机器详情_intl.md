## 1. API Description

Domain name for API request: yunjing.tencentcloudapi.com.

This API (DescribeMachineInfo) is used to get details about a host.

Default request rate limit: 20/sec.

## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/296/19828).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeMachineInfo. |
| Version | Yes | String | Common parameter. The value used for this API: 2/28/2018 |
| Region | No | String | Common parameter. This parameter is not required for this API. |
| Uuid | No | String | Unique Uuid of the HS client. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| MachineIp | String | Host IP. |
| ProtectDays | Integer | Number of days when HS is under protection. |
| MachineOs | String | Operating system. |
| MachineName | String | Host name. |
| MachineStatus | String | Host status.<br/><li>ONLINE: Online</li><li>OFFLINE: Offline</li> |
| InstanceId | String | Unique ID of a CVM or BM. |
| MachineWanIp | String | Host public IP. |
| Quuid | String | Unique Uuid of a CVM or BM. |
| Uuid | String | Unique Uuid of the HS client. |
| IsProVersion | Boolean | Indicates whether HS Pro is activated.<br/><li>true: Yes</li><li>false: No</li> |
| ProVersionOpenDate | String | Time when HS Pro is activated. |
| MachineType | String | Host type.<br/><li>CVM: Cloud virtual machine</li><li>BM: Cloud physical machine</li> |
| MachineRegion | String | Region to which the host belongs, such as ap-guangzhou, and ap-shanghai. |
| PayMode | String | Billing mode.<br/><li>POSTPAY: Postpaid</li><li>PREPAY: Prepaid</li> |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Get details about a host

#### Input example

```
https://yunjing.tencentcloudapi.com/?Action=DescribeMachineInfo
&Uuid=UUID
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "PayMode": "PREPAY",
    "IsProVersion": true,
    "MachineWanIp": "130.111.77.111",
    "Uuid": "e3fcbf68-3bd6-11e8-8954-0819a624c497",
    "RequestId": "ad31cc35-8523-42a2-93e0-b733ad247daa",
    "InstanceId": "ins-ibqb87x3",
    "MachineName": "Developer machine",
    "ProtectDays": 120,
    "MachineRegion": "ap-guangzhou",
    "MachineOs": "3.10.0-327.36.3.el7.x86_64",
    "Quuid": "56af8eea-5a2a-4f0c-81ca-47208e7cd9b2",
    "MachineStatus": "ONLINE",
    "MachineType": "CVM",
    "MachineIp": "10.104.248.0",
    "ProVersionOpenDate": "2018-07-30 12:34:22"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=yunjing&Version=2018-02-28&Action=DescribeMachineInfo)

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

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/296/19830#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter.InvalidFormat | Incorrect parameter format. |
| InvalidParameter.MissingParameter | Missing parameter. |
| InvalidParameter.ParsingError | Parameter parsing error. |
| ResourceNotFound | Resource does not exist. |


## 1. API Description

Domain name for API request: yunjing.tencentcloudapi.com.

This API (DescribeVulInfo) is used to get details about a vulnerability.

Default request rate limit: 20/sec.

## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/296/19828).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeVulInfo. |
| Version | Yes | String | Common parameter. The value used for this API: 2/28/2018 |
| Region | No | String | Common parameter. This parameter is not required for this API. |
| VulId | Yes | Integer | Vulnerability type ID. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| VulId | Integer | Vulnerability type ID. |
| VulName | String | Vulnerability name. |
| VulLevel | String | Vulnerability level. |
| VulType | String | Vulnerability type. |
| Description | String | Vulnerability description. |
| RepairPlan | String | Repair solution. |
| CveId | String | Vulnerability CVE. |
| Reference | String | Reference link. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Get details about a vulnerability

#### Input example

```
https://yunjing.tencentcloudapi.com/?Action=DescribeVulInfo
&VulId=1001
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "CveId": "CVE-001",
    "Description": "Vulnerability description",
    "VulType": "WEB",
    "VulName": "Vulnerability name",
    "VulLevel": "HIGHT",
    "RequestId": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a",
    "VulId": 1001,
    "RepairPlan": "Repair solution",
    "Reference": "http://www.qcloud.com"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=yunjing&Version=2018-02-28&Action=DescribeVulInfo)

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
| InvalidParameter.ParsingError | Parameter parsing error. |
| MissingParameter | A parameter is missing. |
| ResourceNotFound | Resource does not exist. |


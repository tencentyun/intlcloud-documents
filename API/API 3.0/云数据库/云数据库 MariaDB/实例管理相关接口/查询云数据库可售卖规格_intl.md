## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (DescribeDBInstanceSpecs) is used to query the configurations of available database specifications.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeDBInstanceSpecs. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| Specs | Array of [InstanceSpec](/document/api/237/16191#InstanceSpec) | Available specification list by models |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query supported database specifications

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribeDBInstanceSpecs
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "RequestId": "694b99aa-d45e-485e-821b-e84ae16479c2",
    "Specs": [
      {
        "Machine": "TS85",
        "SpecInfos": [
          {
            "Machine": "TS85",
            "MaxStorage": 3000,
            "Memory": 64,
            "MinStorage": 10,
            "NodeCount": 3,
            "Pid": 10820,
            "Qps": 33000,
            "SuitInfo": "Medium Apps with independent users at 1,000k level",
            "TypeName": "Standard"
          },
          {
            "Machine": "TS85",
            "MaxStorage": 3000,
            "Memory": 96,
            "MinStorage": 10,
            "NodeCount": 3,
            "Pid": 10820,
            "Qps": 49000,
            "SuitInfo": "Large-scale Apps with independent users at 10m level",
            "TypeName": "Standard"
          },
          {
            "Machine": "TS85",
            "MaxStorage": 3000,
            "Memory": 120,
            "MinStorage": 10,
            "NodeCount": 3,
            "Pid": 10820,
            "Qps": 61000,
            "SuitInfo": "Large-scale Apps with independent users at 10m level",
            "TypeName": "Standard"
          }
        ]
      }
    ]
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=DescribeDBInstanceSpecs)

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

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/237/16149#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.DbOperationFailed | Failed to query the database |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |


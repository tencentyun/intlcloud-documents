## 1. API Description

API request domain name: scf.tencentcloudapi.com.

This API returns a list of function based on the query parameters。

Default API request frequency limit: 20 times/second.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/583/17238).


| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ListFunctions |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-16 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/583/17238#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| Order | No | String | Sorting query results in either ascending or descending order; valid values: ASC and DESC |
| Orderby | No | String | Sorting the query results in either ascending or descending according to one or more fields, including AddTime, ModTime, FunctionName |
| Offset | No | Integer | Data offset; 0 by default |
| Limit | No | Integer | Length of the returned data; 20 by default |
| SearchKey | No | String | Fuzzy function name matching |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Functions | Array of [Function](/document/api/583/17244#Function) | Function list |
| TotalCount | Integer | Total number of query results |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Getting a List of Function with Specified Criteria

#### Input Sample Code

```
https://scf.tencentcloudapi.com/?Action=ListFunctions
&Limit=2
&Order=ASC
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "Functions": [
            {
                "FunctionId": "lam-xxxxxxx",
                "Namespace": "default",
                "FunctionName": "test",
                "ModTime": "2018-04-08 19:02:20",
                "AddTime": "2018-04-08 15:18:49",
                "Runtime": "Python2.7"            
            }
        ],
        "TotalCount": 1,
        "RequestID": "3c140219-cfe9-470e-b241-907877d6fb03"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=scf&Version=2018-04-16&Action=ListFunctions)

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

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/583/17240#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameterValue | An invalid value was declared for the input parameter. |
| InvalidParameterValue.Order | An invalid value was declared for the input parameter: Order. |
| InvalidParameterValue.Orderby | An invalid value was declared for the input parameter: Orderby |
| UnauthorizedOperation.CAM | CAM authentication failed. |
| UnauthorizedOperation.Region | Error with Region. |


## 1. API Description

API request domain name: scf.tencentcloudapi.com.

This API creates a user-defined function with declared parameters.

Default API request frequency limit: 10 times/second.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/583/17238).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: CreateFunction |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-16 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/583/17238#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| FunctionName | Yes | String | Name of the new function. The name: must be between 2 and 60 characters long; can contain any letters (both uppercase and lowercase) from a to z and any numbers from 0 through 9; can contain some special characters, including hyphen or dash, and underscore; must begin with a letter and be unique, and must not end with an underscore or a dash. |
| Code | Yes | [Code](/document/api/583/17244#Code) | Function code. Note: COS and ZipFile cannot be specified at the same time |
| Handler | No | String | Name of the handler. A handler is a method that the runtime executes when your function is invoked. A handler name must be formatted as the function name following the file name with a period (.) between these two names, for example, FileName.FunctionName. <br> Both file name and function name: must be between 2 and 60 characters long; can contain any letters (both uppercase and lowercase) from a to z and any numbers from 0 through 9, can contain some special characters, including hyphen or dash, and underscore; must begin and end with a letter. |
| Description | No | String | Description of the function. The description can be up to 1,000 characters long and can contain any letters (both uppercase and lowercase) from a to z, any numbers from 0 through 9, spaces, line breaks, commas and period. Chinese characters are also supported. |
| MemorySize | No | Integer | The size of memory size available to the function during execution. Specify a value between 128 MB (default) and 1,536 MB in 128 MB increments. |
| Timeout | No | Integer | The duration a function allowed to execute. Choose a value between 1 and 300 seconds;  The default is 3 seconds. |
| Environment | No | [Environment](/document/api/583/17244#Environment) | Environment variable of the function |
| Runtime | No | String | Runtime environment of the function; supported environment: Python2.7 (default), Python3.6, Nodejs6.10, PHP5, PHP7, Golang1 and Java8. |
| VpcConfig | No | [VpcConfig](/document/api/583/17244#VpcConfig) | VPC configuration of the function |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Creating a Function

#### Input Sample Code

```
https://scf.tencentcloudapi.com/?Action=CreateFunction
&FunctionName=<FunctionName>
&Handler=<function.handler>
&Code.CosBucketName=<CosBucketName>
&Code.CosObjectName=<CosObjectName>
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "RequestId": "eac6b301-a322-493a-8e36-83b295459397"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=scf&Version=2018-04-16&Action=CreateFunction)

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
| InternalError | Internal error |
| InternalError.System | Internal system error. |
| InvalidParameterValue | An invalid value was declared for the input parameter. |
| InvalidParameterValue.Code | An invalid value was declared for the input parameter: Code. |
| InvalidParameterValue.Description | An invalid value was declared for the input parameter: Description. |
| InvalidParameterValue.Environment | An invalid value was declared for the input parameter: Environment. |
| InvalidParameterValue.FunctionName | Function does not exist. |
| InvalidParameterValue.Handler | An invalid value was declared for the input parameter: Handler. |
| InvalidParameterValue.Runtime | An invalid value was declared for the input parameter: Runtime |
| LimitExceeded.Function | The number of functions exceeds the upper limit. |
| LimitExceeded.Memory | Memory exceeds the upper limit. |
| LimitExceeded.Timeout | Timeout exceeds the upper limit. |
| MissingParameter.Code | The parameter Code was missing. |
| ResourceInUse.FunctionName | FunctionName already exists. |
| UnauthorizedOperation.CAM | CAM authentication failed. |
| UnauthorizedOperation.Region | Error with Region. |


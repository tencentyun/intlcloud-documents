## 1. API Description

API request domain name: scf.tencentcloudapi.com.

This API gets the function details, including fields such as the name, code, handling method, associated trigger and timeout.

Default API request frequency limit: 20 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/583/17238).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: GetFunction |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-16 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/583/17238#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| FunctionName | Yes | String | Name of the queried function |
| Qualifier | No | String | Version number of the function |
| ShowCode | No | String | Whether or not to display the code; TRUE means yes, while FALSE means no; any code that is larger than 1MB in size will not be displayed. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| ModTime | Timestamp | Last modified time of the function |
| CodeInfo | String | Code of the function |
| Description | String | Description of the function |
| Triggers | Array of [Trigger](/document/api/583/17244#Trigger) | Trigger list of the function |
| Handler | String | Handler of the function |
| CodeSize | Integer | Code size of the function |
| Timeout | Integer | Timeout of the function |
| FunctionVersion | String | Version of the function |
| MemorySize | Integer | Maximum available memory for the function |
| Runtime | String | Runtime environment of the function |
| FunctionName | String | Name of the function |
| VpcConfig | [VpcConfig](/document/api/583/17244#VpcConfig) | VPC of the function |
| UseGpu | String | This indicates whether to use the GPU |
| Environment | [Environment](/document/api/583/17244#Environment) | Environment variables of the function |
| CodeResult | String | This indicates whether the code is correct |
| CodeError | String | Error message of the code |
| ErrNo | Integer | Error code of the code |
| Namespace | String | Namespace of the function |
| Role | String | Role bound with the function |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |


## 4. Sample

### Getting Function Details

You use this function to get the corresponding function information, and you can specify the version and namespace.

#### Input Sample Code

```
https://scf.tencentcloudapi.com/?Action=GetFunction
&FunctionName=<FunctionName>
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "ModTime": "2018-06-07 09:52:23",
        "Environment": {
            "Variables": []
        },
        "CodeError": "",
        "Description": "",
        "VpcConfig": {
            "SubnetId": "",
            "VpcId": ""
        },
        "Triggers": [],
        "ErrNo": 0,
        "UseGpu": "FALSE",
        "CodeSize": 0,
        "MemorySize": 128,
        "Namespace": "default",
        "FunctionVersion": "$LATEST",
        "Timeout": 3,
        "RequestId": "a1ffbba5-5489-45bc-89c5-453e50d5386e",
        "CodeResult": "failed",
        "Handler": "scfredis.main_handler",
        "Runtime": "Python2.7",
        "FunctionName": "ledDummyAPITest",
        "CodeInfo": "",
        "Role": ""
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=scf&Version=2018-04-16&Action=GetFunction)

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
| ResourceNotFound.FunctionName | Function does not exist. |
| UnauthorizedOperation | Unauthorized operation |
| UnauthorizedOperation.CAM | CAM authentication failed. |


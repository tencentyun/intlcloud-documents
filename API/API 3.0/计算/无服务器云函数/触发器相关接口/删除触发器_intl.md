## 1. API Description

API request domain name: scf.tencentcloudapi.com.

The API deletes the existing trigger based on the input parameters.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/583/17238).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DeleteTrigger |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-16 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/583/17238#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| FunctionName | Yes | String | Name of the function |
| TriggerName | Yes | String | Name of the trigger to be deleted |
| Type | Yes | String | Type of the trigger to be deleted; currently, COS, CMQ, timer and CKafka types are supported |
| TriggerDesc | No | String | If the to-be-deleted trigger is a COS trigger, this field is a required and holds the data {"event":"cos:ObjectCreated: \*"} in JSON format, and the data content is in the same format as this field in the CreateTrigger API; if the to-be-deleted trigger is a timer or CMQ trigger, this field is optional |
| Qualifier | No | String | Version information of the function |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Deleting a Trigger

You use this function to delete a trigger.

#### Input Sample Code

```
https://scf.tencentcloudapi.com/?Action=DeleteTrigger
&FunctionName=ledDummyAPITest
&TriggerName=test3
&Type=timer
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

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=scf&Version=2018-04-16&Action=DeleteTrigger)

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

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/583/17240#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InternalError.System | Internal system error. |
| InvalidParameterValue | Wrong parameter value |
| InvalidParameterValue.Cdn |An invalid value was declared for the input parameter: Cdn |
| InvalidParameterValue.Cmq | An invalid value was declared for the input parameter: CKafka |
| InvalidParameterValue.Cos | An invalid value was declared for the input parameter: COS||
| ResourceInUse.Cdn | CDN is in use. |
| ResourceInUse.Cmq | CMQ is in use. |
| ResourceNotFound.Cdn | CDN does not exist. |
| ResourceNotFound.Cmq | CMQ does not exist. |
| ResourceNotFound.FunctionName | Function does not exist. |
| UnauthorizedOperation.CAM | CAM authentication failed. |
| UnsupportedOperation.Cdn | CDN is not supported. |


## 1. API Description

API request domain name: scf.tencentcloudapi.com.

The API creates a new trigger based on the input parameters.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/583/17238).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: CreateTrigger |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-16 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/583/17238#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| FunctionName | Yes | String | Name of the function bound with the new trigger |
| TriggerName | Yes | String | Name of the new trigger. For a timer trigger, the name supports up to 100 characters including letters, numbers, dashes and underscores; for other triggers, see the descriptions of parameters bound with the specific trigger |
| Type | Yes | String | Type of the trigger; currently, COS, CMQ, timer and CKafka types are supported |
| TriggerDesc | No| String | The parameter corresponding to the trigger. For a timer trigger, its content is a Linux cron expression; for other triggers, see the description of the specific trigger |
| Qualifier | No | String | Version of the function |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Sample

### Creating a Trigger

You use this function to create a trigger.

#### Input Sample Code

```
https://scf.tencentcloudapi.com/?Action=CreateTrigger
&FunctionName=<FunctionName>
&TriggleName=<TriggerName>
&Type=timer
&TriggerDesc=*/2****
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

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=scf&Version=2018-04-16&Action=CreateTrigger)

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
| InternalError.System | Internal system error. |
| InvalidParameterValue | An invalid value was declared for the input parameter. |
| InvalidParameterValue.Cdn |An invalid value was declared for the input parameter: Cdn |
| InvalidParameterValue.Ckafka | An invalid value was declared for the input parameter: CKafka |
| InvalidParameterValue.Cos | An invalid value was declared for the input parameter: COS|
| InvalidParameterValue.TriggerDesc | An invalid value was declared for the input parameter: TriggerDesc |
| InvalidParameterValue.TriggerName | An invalid value was declared for the input parameter: TriggerName |
| InvalidParameterValue.Type | An invalid value was declared for the input parameter: Type |
| LimitExceeded.Cdn | CDN usage exceeds the upper limit. |
| LimitExceeded.FunctionOnTopic | The number of functions under the same topic exceeds the upper limit. |
| LimitExceeded.Trigger | The number of triggers exceeds the upper limit. |
| ResourceInUse.Cdn | CDN is in use. |
| ResourceInUse.Cmq | CMQ is in use. |
| ResourceInUse.Cos | COS is in use. |
| ResourceNotFound.Cdn | CDN does not exist. |
| ResourceNotFound.Ckafka | CKafka does not exist. |
| ResourceNotFound.Cmq | CMQ does not exist. |
| ResourceNotFound.Cos | COS does not exist. |
| ResourceNotFound.FunctionName | Function does not exist. |
| ResourceNotFound.FunctionVersion | Function version does not exist. |
| UnauthorizedOperation.CAM | CAM authentication failed. |
| UnsupportedOperation.Cdn | CDN is not supported. |
| UnsupportedOperation.Cos | COS operation is not supported. |
| UnsupportedOperation.Trigger | Trigger operation is not supported. |


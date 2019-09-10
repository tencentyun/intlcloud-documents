## 1. API Description

API domain name: as.tencentcloudapi.com.

This API (CompleteLifecycleAction) is used to perform the action to complete the lifecycle.

* The result ("CONTINUE" or "ABANDON") of a specific lifecycle hook can be specified by calling this API. If this API is not called at all, the lifecycle hook will be processed based on the "DefaultResult" after timeout.


Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if the common parameter `Region` is a financial region such as ap-shanghai-fsi, it is necessary to specify a domain name with a financial region, preferably the same as that specified in `Region`, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/377/20426).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: CompleteLifecycleAction |
| Version | Yes | String | Common parameter. The value used for this API: 2018-04-19 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/377/20426#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| LifecycleHookId | Yes | String | Lifecycle hook ID |
| LifecycleActionResult | Yes | String | Result of the lifecycle action. Value range: "CONTINUE", "ABANDON" |
| InstanceId | No | String | Instance ID. Either "InstanceId" or "LifecycleActionToken" must be specified |
| LifecycleActionToken | No | String | Either "InstanceId" or "LifecycleActionToken" must be specified |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Completing a Lifecycle Action by Calling with InstanceId

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CompleteLifecycleAction
&LifecycleHookId=ash-fbjiexz7
&InstanceId=ins-ni8bpmve
&LifecycleActionResult=CONTINUE
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "d0cf47b9-4236-491c-bfab-106947198afe"
  }
}
```

### Sample 2. Completing a Lifecycle Action by Calling with LifecycleActionToken

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=CompleteLifecycleAction
&LifecycleHookId=ash-fbjiexz7
&LifecycleActionToken=4d910016-2590-444d-8f4a-c14940036902
&LifecycleActionResult=CONTINUE
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "de792ffe-e37e-4f1d-8534-300b555739da"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=CompleteLifecycleAction)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/377/20428#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter | Incorrect parameter |
| InvalidParameterValue | Invalid parameter value |
| ResourceNotFound.LifecycleHookInstanceNotFound | The instance corresponding to the lifecycle hook does not exist. |
| ResourceNotFound.LifecycleHookNotFound | The specified lifecycle hook was not found. |
| ResourceUnavailable.LifecycleActionResultHasSet | The lifecycle action has already been set. |

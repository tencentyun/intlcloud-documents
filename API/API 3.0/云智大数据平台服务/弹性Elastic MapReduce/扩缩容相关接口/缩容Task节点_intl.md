## 1. API Description

API domain name: emr.tencentcloudapi.com.

This API terminates one or more task nodes.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/589/33974).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: TerminateTasks |
| Version | Yes | String | Common parameter. The version of this API: 2019-01-03 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/589/33974#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | ID of the instance to which the terminated node belongs |
| ResourceIds.N | Yes | Array of String | ID of the terminated node |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Result | [TerminateResult](/document/api/589/33981#TerminateResult) | Termination result |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1. Terminating a Node

Terminate a task node

#### Input Sample Code

```
https://emr.tencentcloudapi.com/?Action=TerminateTasks
&InstanceId=emr-4slr7ad7
&ResourceIds.0=emr-vm-xxx33tg
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Result": {
      "InstanceId": "emr-4slr7ad7",
      "ResourceIds": [
        "emr-vm-xxx33tg"
      ]
    },
    "RequestId": "4d701c1e-8507-47e1-8c69-a8f06a236f24"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=emr&Version=2019-01-03&Action=TerminateTasks)

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

This API has no error codes related to business logic. For other error codes, see [Common Error Codes](/document/api/589/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

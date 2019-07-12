## 1. API Description

API domain name: emr.tencentcloudapi.com.

This API scales out the specified instance.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/589/33974).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: ScaleOutInstance |
| Version | Yes | String | Common parameter. The value used for this API: 2019-01-03 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/589/33974#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| ClientToken | Yes | String | Token |
| TimeUnit | Yes | String | Time unit |
| TimeSpan | Yes | Integer | Time span |
| InstanceId | Yes | String | ID of the instance for scale-out |
| PayMode | Yes | Integer | Payment method |
| PreExecutedFileSettings | No | [PreExecuteFileSettings](/document/api/589/33981#PreExecuteFileSettings) | Pre-execution script settings |
| TaskCount | No | Integer | Number of task nodes to add |
| CoreCount | No | Integer | Number of core nodes to add |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Result | [ScaleOutInstanceResult](/document/api/589/33981#ScaleOutInstanceResult) | Scale-out result |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Examples

### Example 1. Scaling out an Instance

#### Input Sample Code

```
https://emr.tencentcloudapi.com/?Action=ScaleOutInstance
&ClientToken=jaco3
&TimeUnit=m
&TimeSpan=1
&TaskCount=1
&InstanceId=emr-b3zor8nr
&PayMode=0
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "Result": {
      "ClientToken": "jaco3",
      "InstanceId": "emr-b3zor8nr",
      "DealNames": [
        "20190314262369",
        "20190314262370",
        "20190314262371",
        "20190314262372"
      ]
    },
    "RequestId": "e00a062d-dfea-4e6e-9de7-8fbc8c7971ab"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=emr&Version=2019-01-03&Action=ScaleOutInstance)

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

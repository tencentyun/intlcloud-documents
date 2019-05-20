## 1. API Description
API request domain name: scf.tencentcloudapi.com.
The API is used to delete the existing trigger based on the parameters passed in.
Default API request frequency limit: 100 times/second.
## 2. Input Parameters
The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/583/17238).
| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DeleteTrigger |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-16 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/583/17238#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| FunctionName | Yes | String | Name of the function |
| TriggerName | Yes | String | Name of the trigger to be deleted |
| Type | Yes | String | Type of the trigger to be deleted; currently, COS, CMQ, timer and CKafka types are supported |
| TriggerDesc | No | String | If the to-be-deleted trigger is a COS trigger, this field is a required and holds the data {"event":"cos:ObjectCreated:*"} in JSON format, and the data content is in the same format as this field in the CreateTrigger API; if the to-be-deleted trigger is a timer or CMQ trigger, this field is optional |
| Qualifier | No | String | Version information of the function |
## 3. Output Parameters
| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |
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
**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**
* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=scf&Version=2018-04-16&Action=DeleteTrigger)
### SDK
Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.
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
| InvalidParameterValue.Cdn | Wrong CDN parameter passed in. |
| InvalidParameterValue.Cmq | Wrong CMQ parameter passed in. |
| InvalidParameterValue.Cos | Wrong COS parameter passed in. |
| ResourceInUse.Cdn | CDN is in use. |
| ResourceInUse.Cmq | CMQ is in use. |
| ResourceNotFound.Cdn | CDN does not exist. |
| ResourceNotFound.Cmq | CMQ does not exist. |
| ResourceNotFound.FunctionName | Function does not exist. |
| UnauthorizedOperation.CAM | CAM authentication failed. |
| UnsupportedOperation.Cdn | CDN is not supported. |


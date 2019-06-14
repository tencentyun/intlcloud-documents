## 1. API Description

API domain name: cam.tencentcloudapi.com.

This API (CreatePolicy) creates a policy.

Default API request rate limit: 10 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/598/33158).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: CreatePolicy |
| Version | Yes | String | Common parameter; the version of this API: 2019-01-16 |
| Region | No | String | Common parameter; optional for this API. |
| PolicyName | Yes | String | Policy name |
| PolicyDocument | Yes | String | Policy document |
| Description | No | String | Policy description |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| PolicyId | Integer | ID of the new policy |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Creating a Policy

The example below creates a policy that allows all COS APIs to access all COS resources

#### Input Sample Code

```
https://cam.tencentcloudapi.com/?Action=CreatePolicy
&PolicyName=test-2019-04-29
&Description=%E6%B5%8B%E8%AF%95%E7%AD%96%E7%95%A5
&PolicyDocument=%7B%22version%22%3A%222.0%22%2C%22statement%22%3A%5B%7B%22effect%22%3A%22allow%22%2C%22action%22%3A%5B%22name%2Fcos%3A%2A%22%5D%2C%22resource%22%3A%5B%22%2A%22%5D%7D%5D%7D
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "PolicyId": 17698703,
    "RequestId": "89360f78-b1dd-4e43-aa91-ecb2c8b8f282"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=CreatePolicy)

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

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/598/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.PolicyFull | The number of user policies exceeds the upper limit. |
| FailedOperation.PolicyNameInUse | The policy name specified by the PolicyName field already exists. |
| InternalError.SystemError | Internal error. |
| InvalidParameter.ActionError | The Action field of the policy document is invalid. |
| InvalidParameter.AttachmentFull | The number of policies associated with the authorization object of the principal field has reached the upper limit. |
| InvalidParameter.ConditionError | The condition field of the policy document is invalid. |
| InvalidParameter.DescriptionLengthOverlimit | The input parameter Description cannot exceed 300 bytes in length. |
| InvalidParameter.EffectError | The Effect field of the policy document is invalid. |
| InvalidParameter.NotSupportProduct | CAM does not support the resource type specified in the policy document. |
| InvalidParameter.ParamError | Invalid input parameter. |
| InvalidParameter.PolicyDocumentError | The PolicyDocument field is invalid. |
| InvalidParameter.PolicyDocumentLengthOverLimit | The PolicyDocument field exceeds the length limit. |
| InvalidParameter.PolicyNameError | The PolicyName field is invalid. |
| InvalidParameter.PrincipalError | The principal field of the policy document is invalid. |
| InvalidParameter.ResourceError | The Resource field of the policy document is invalid. |
| InvalidParameter.StatementError | The Statement field of the policy document is invalid. |
| InvalidParameter.UserNotExist | The authorization object of the principal field does not exist. |
| InvalidParameter.VersionError | The Version field of the policy document is invalid. |
| ResourceNotFound.GroupNotExist | The user group does not exist. |
| ResourceNotFound.NotFound | The resource does not exist. |
| ResourceNotFound.UserNotExist | The user does not exist. |
## 1. API Description

API request domain name: iotcloud.tencentcloudapi.com.

This API (CreateTopicRule) is used to create a rule.

Default API request frequency limit: 100 times/second.

## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](https://cloud.tencent.com/document/api/634/19472).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: CreateTopicRule |
| Version | Yes | String | Common parameter; the value for this API: 2018-06-14 |
| Region | No | String | Common parameter; not passed for this API |
| RuleName | Yes | String | Rule name |
| TopicRulePayload | Yes | [TopicRulePayload](https://cloud.tencent.com/document/api/634/19497#TopicRulePayload) | Rule content |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Creating a Rule

#### Input Example

```
https://iotcloud.tencentcloudapi.com/?Action=CreateTopicRule
&RuleName=testrulename
&TopicRulePayload.SQL=U0VMRUNUIGZpZWxkMSwgZmllbGQyIEZST00gJ3NyY1Byb2R1Y3RJZC9zcmNEZXZpY2VOYW1lL2V2ZW50Jw==
&TopicRulePayload.Actions=[]
&TopicRule.Description=test
&TopicRule.RuleDisabled=false
&<Common request parameter>
```

#### Output Example

```
{
  "Response": {
    "RequestId": "be69a7a3-7315-40a7-9532-3316e4a3e97e"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using Cloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=iotcloud&Version=2018-06-14&Action=CreateTopicRule)

### SDK

Cloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)

## 6. Error Codes

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/634/19474#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameterValue | Wrong parameter value |
| InvalidParameterValue.InvalidSQL | The SQL statement contains invalid characters. |
| InvalidParameterValue.TopicRuleAlreadyExist | The rule already exists. |

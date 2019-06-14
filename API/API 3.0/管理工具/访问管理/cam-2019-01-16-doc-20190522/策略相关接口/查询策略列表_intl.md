## 1. API Description

API domain name: cam.tencentcloudapi.com.

This API (ListPolicies) queries the list of policies.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/598/33158).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: ListPolicies |
| Version | Yes | String | Common parameter; the version of this API: 2019-01-16 |
| Region | No | String | Common parameter; optional for this API. |
| Rp | No | Integer | Quantity per page; 20 by default; the value must be greater than 0 and less than or equal to 200 |
| Page | No | Integer | Page number starting from 1; 1 by default; up to 200 |
| Scope | No | String | Value range: All, QCS, and Local. "All" indicates to get all policies; "QCS" indicates to get predefined policies only; and "Local" indicates to get custom policies only. "All" is the default value. |
| Keyword | No | String | Filter by policy name |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalNum | Integer | Total number of policies |
| List | Array of [StrategyInfo](/document/api/598/33167#StrategyInfo) | Policy array. Each array contains fields such as policyId, policyName, addTime, type, description, and createMode. <br/>policyId: Policy ID <br/>policyName: Policy name <br/>addTime: Creation time of the policy <br/>type: 1 means custom policy; 2 means predefined policy <br/>description: Policy description <br/>createMode: 1 indicates to create a policy by business permissions; other values indicate to view policy syntax and update policies through policy syntax |
| ServiceTypeList | Array of String | Reserved field <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Sample 1. Viewing Policy List

#### Input Sample Code

```
https://cam.tencentcloudapi.com/?Action=ListPolicies
&Rp=1
&Page=10
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "ServiceTypeList": [],
    "List": [
      {
        "PolicyId": 16313162,
        "PolicyName": "QcloudAccessForCDNRole",
        "AddTime": "2019-04-19 10:55:31",
        "Type": 2,
        "Description": "CDN permissions (including but not limited to): CLS (create/read/update/delete CLS logsets/log topics, and search for/download/upload logs)." ,
        "CreateMode": 2,
        "Attachments": 0,
        "ServiceType": "cooperator"
      }
    ],
    "TotalNum": 239,
    "RequestId": "ae2bd2b7-1d55-4b0a-8154-e02407a2b390"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cam&Version=2019-01-16&Action=ListPolicies)

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
| InternalError.SystemError | Internal error. |
| InvalidParameter.GroupIdError | The GroupId field is invalid. |
| InvalidParameter.KeywordError | The Keyword field is invalid. |
| InvalidParameter.ParamError | Invalid input parameter. |
| InvalidParameter.ScopeError | The Scope field is invalid. |
| InvalidParameter.ServiceTypeError | The ServiceType field is invalid. |
| InvalidParameter.UinError | The Uin field is invalid. |
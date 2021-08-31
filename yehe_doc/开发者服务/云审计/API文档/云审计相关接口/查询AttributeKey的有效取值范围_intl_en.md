## 1. API Description

API domain name: cloudaudit.tencentcloudapi.com.

This API is used to query the valid values of AttributeKey.

Default API request rate limit: 20 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, please see [Common Request Parameters](https://intl.cloud.tencent.com/document/api/1021/34192).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: GetAttributeKey. |
| Version | Yes | String | Common parameter. The value used for this API: 2019-03-19. |
| Region | Yes | String | Common parameter. For more information, please see the [list of regions](https://intl.cloud.tencent.com/document/api/1021/34192#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| WebsiteType | No | String | Website type. Valid values: zh, en. Default value: zh |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| AttributeKeyDetails | Array of [AttributeKeyDetail](https://intl.cloud.tencent.com/document/api/1021/34209#AttributeKeyDetail) | Valid values of AttributeKey |
| RequestId | String | Unique ID of request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. |

## 4. Samples

### Sample 1. Querying the valid values of AttributeKey

This example shows you how to query the valid values of AttributeKey.

#### Input sample code

```
https://cloudaudit.tencentcloudapi.com/?Action=GetAttributeKey
&WebsiteType=zh
&<Common request parameters>
```

#### Output sample code

```
{
  "Response": {
    "RequestId": "6d833833-bbc6-4463-9a8f-6cc62d3a2afd",
    "AttributeKeyDetails": [
      {
        "Label": "Read-only",
        "Value": "ReadOnly",
        "Starter": "Select the read-only value",
        "LabelType": "select",
        "Order": 1
      },
      {
        "Label": "Access key",
        "Value": "AccessKeyId",
        "Starter": "Enter the access key",
        "LabelType": "text",
        "Order": 2
      },
      {
        "Label": "Request ID",
        "Value": "RequestId",
        "Starter": "Enter the request ID",
        "LabelType": "text",
        "Order": 3
      },
      {
        "Label": "Event name",
        "Value": "EventName",
        "Starter": "Select the event name",
        "LabelType": "select",
        "Order": 4
      },
      {
        "Label": "Resource name",
        "Value": "ResourceName",
        "Starter": "Enter the resource name",
        "LabelType": "text",
        "Order": 5
      },
      {
        "Label": "Resource type",
        "Value": "ResourceType",
        "Starter": "Select the resource type",
        "LabelType": "select",
        "Order": 6
      },
      {
        "Label": "Username",
        "Value": "Username",
        "Starter": "Select the username",
        "LabelType": "select",
        "Order": 7
      }
    ]
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool allows online call, signature authentication, SDK code generation, and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cloudaudit&Version=2019-03-19&Action=GetAttributeKey)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for Node.js](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, please see [Common Error Codes](https://intl.cloud.tencent.com/document/api/1021/34195#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.SearchError | Internal error. Please submit a ticket. |

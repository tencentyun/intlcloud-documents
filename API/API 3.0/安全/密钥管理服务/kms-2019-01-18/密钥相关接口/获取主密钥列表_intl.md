## 1. API Description

API domain name: kms.tencentcloudapi.com

This API describes the keys (KeyIds) under the specified account.

API request rate limit: 50 requests/sec.

## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/573/34406).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: ListKeys |
| Version | Yes | String | Common parameter. The version of this API: 2019-01-18 |
| Region | Yes | String | Common parameter. For more information, see the [List of Regions](/document/api/573/34406#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Offset | No | Integer | This parameter is the same as Offset in SQL, indicating the starting point to return rows from an ordered result set. Default value is 0 |
| Limit | No | Integer | This parameter has the same meaning of the Limit in an SQL query, indicating that up to "Limit value" elements can be obtained this time. The default value is 10 and the maximum value is 200 |
| Role | No | Integer | Filter by creator role. 0 (default value): the CMK is created by the user; 1: the CMK is created automatically by an authorized Tencent Cloud product |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| Keys | Array of [Key](/document/api/573/34431#Key) | CMK list array <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| TotalCount | Integer | Total number of CMKs |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Examples

### Example 1. Getting CMK List

Get the CMK list

#### Input Sample Code

```
https://kms.tencentcloudapi.com/?Action=ListKeys
&Offset=0
&Limit=2
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RequestId": "1b580852-1e38-11e9-b129-5cb9019b4b00",
    "Keys": [
      {
        "KeyId": "23e80852-1e38-11e9-b129-5cb9019b4b01"
      },
      {
        "KeyId": "23e80852-1e38-11e9-b129-5cb9019b4b02"
      }
    ],
    "TotalCount": 100
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool makes it easy for you to call Tencent Cloud APIs,  authenticate signature, generate SDK codes, and search for APIs. **

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=kms&Version=2019-01-18&Action=ListKeys)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) for various programming languages, facilitating API calls. 

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/573/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter | Incorrect parameter. |
| UnauthorizedOperation | Unauthorized operation. |

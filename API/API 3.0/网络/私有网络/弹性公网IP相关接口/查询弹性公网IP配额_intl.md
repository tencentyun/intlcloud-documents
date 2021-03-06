## 1. API Description

Domain name for API request: vpc.tencentcloudapi.com.

This API (DescribeAddressQuota) is used to query the quota information of [Elastic IPs](https://intl.cloud.tencent.com/document/product/213/5733) (EIP) in your account in the current region. For more information about EIP quota, see [Overview of EIP Products](https://intl.cloud.tencent.com/document/product/213/5733).

A maximum of 10 requests can be initiated per second for this API.

Note: This API supports Finance regions. Since Finance regions and non-Finance regions are isolated and not interconnected. If the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region that should be identical to the value of Region field, for example: vpc.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](https://cloud.tencent.com/document/api/215/15692).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeAddressQuota |
| Version | Yes |  String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes |  String | Common parameter. For more information, please see the [list of regions](https://cloud.tencent.comhttps://cloud.tencent.com/document/api/215/15692#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| QuotaSet | Array of [Quota](https://cloud.tencent.com/document/api/215/##Quota) | The quota information of EIPs in an account. |
| RequestId | String | The unique request ID, which is returned for each request. RequestId is required for locating a problem. |

## 4. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](https://cloud.tencent.com/document/api/215/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalServerError | Internal error. |

## 5. Example

### Example 1 Query EIP quotas

#### Input example

```
https://vpc.tencentcloudapi.com/?Action=DescribeAddressQuota
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "QuotaSet": [
      {
        "QuotaCurrent": 0,
        "QuotaId": "TOTAL_EIP_QUOTA",
        "QuotaLimit": 20
      },
      {
        "QuotaCurrent": 0,
        "QuotaId": "DAILY_EIP_APPLY",
        "QuotaLimit": 40
      },
      {
        "QuotaCurrent": 0,
        "QuotaId": "DAILY_EIP_ASSIGN",
        "QuotaLimit": 40
      }
    ],
    "RequestId": "6EF60BEC-0242-43AF-BB20-270359FB54A7"
  }
}
```


## 6. Other Resources

Cloud API 3.0 comes with the following development tools to make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
* [Tencent Cloud CLI 3.0](https://intl.cloud.tencent.com/document/product/1013/33463)


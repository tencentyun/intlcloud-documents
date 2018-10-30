## 1. API Description

Domain name for API request: mariadb.tencentcloudapi.com

This API (DescribePrice) is used to query the price of an instance before purchasing it.

Default request rate limit: 20/sec.

Note: This API supports Finance regions. Finance and non-Finance regions are isolated from each other. Therefore, if the common parameter Region is a Finance region (such as ap-shanghai-fsi), you need to specify a domain name containing the Finance region specified in the Region field, for example: mariadb.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following request parameter list only provides API request parameters and some common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/237/16147).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value​used for this API: DescribePrice. |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12. |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/237/16147#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Zone | Yes | String | Availability zone ID of an instance to be purchased |
| NodeCount | Yes | Integer | Number of instance nodes, which can be obtained by querying instance specification <br/>(DescribeDBInstanceSpecs). |
| Memory | Yes | Integer | Memory (in GB), which can be obtained by querying instance specification <br/>(DescribeDBInstanceSpecs). |
| Storage | Yes | Integer | Storage space (in GB). You can query the instance specification using DescribeDBInstanceSpecs<br/> to get the lower limit and upper limit of the disk for different memory sizes. |
| Period | No | Integer | Usage period to be purchased (in month) |
| Count | No | Integer | Quantity to be purchased. The price of one instance is queried by default. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| OriginalPrice | Integer | Original price (in 0.01 CNY) |
| Price | Integer | Actual price (in 0.01 CNY). It may be different from the original price depending on the discount. |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Example

### Example 1 Query the price of a newly purchased database instance

#### Input example

```
https://mariadb.tencentcloudapi.com/?Action=DescribePrice
&NodeCount=2
&Memory=2000
&Storage=10000
&Zone=ap-guangzhou-2
&Count=1
&Period=1
&<Common request parameters>
```

#### Output example

```
{
  "Response": {
    "OriginalPrice": 21120,
    "Price": 21120,
    "RequestId": "7e1000c2-190a-d0df-ff75-59fbdf5ff381"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick indexing of APIs to greatly improve the efficiency of using cloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=mariadb&Version=2017-03-12&Action=DescribePrice)

### SDK

Cloud API 3.0 comes with the software development kit (SDK) that supports multiple programming languages and makes it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to the API business logic. For other error codes, see [Common Error Codes](/document/api/237/16149#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError.CamAuthFailed | CAM authentication request failed |
| InternalError.QueryPriceFailed | Failed to query the price |
| InvalidParameter.GenericParameterError | Failed to pass the parameter validity verification |
| InvalidParameterValue.SpecIdIllegal | No specification of a database instance found |
| UnauthorizedOperation.PermissionDenied | No permission to perform operations on the API or resource |


## **1. API Description**
API request domain name: batch.tencentcloudapi.com.

This API is used to get model configuration information of the availability zone of Batch

Default API request frequency limit: 2 times/second.



## **2. Input Parameters**

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/599/15883).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeCvmZoneInstanceConfigInfos |
| Version | Yes | String | Common parameter; the value for this API: 2017-03-12 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/599/15883#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Filters | No | [Filter](/document/api/599/15912#Filter) | Filters |

## **3. Output Parameters**

| Parameter name | Type | Description |
|---------|---------|---------|
| InstanceTypeQuotaSet | Array of [InstanceTypeQuotaItem](/document/api/599/15912#InstanceTypeQuotaItem) | List of model configurations in the availability zone. |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Configuration Information of Postpaid Models in Chongqing Zone 1

#### Input

```
https://batch.tencentcloudapi.com/?Action=DescribeCvmZoneInstanceConfigInfos
&Filters.0.Name=zone
&Filters.0.Values.0=ap-chongqing-1
&Filters.1.Name=instance-charge-type
&Filters.1.Values.0=POSTPAID_BY_HOUR
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "InstanceTypeQuotaSet": [
      {
        "Cpu": 1,
        "Externals": {},
        "InstanceChargeType": "POSTPAID_BY_HOUR",
        "InstanceFamily": "S3",
        "InstanceQuota": 1999,
        "InstanceType": "S3.SMALL1",
        "LocalDiskTypeList": [],
        "Memory": 1,
        "NetworkCard": 0,
        "Price": {
          "ChargeUnit": "HOUR",
          "UnitPrice": 0.18
        },
        "Status": "SELL",
        "TypeName": "Standard S3",
        "Zone": "ap-chongqing-1"
      },
      {
        "Cpu": 1,
        "Externals": {},
        "InstanceChargeType": "POSTPAID_BY_HOUR",
        "InstanceFamily": "S3",
        "InstanceQuota": 1999,
        "InstanceType": "S3.SMALL2",
        "LocalDiskTypeList": [],
        "Memory": 2,
        "NetworkCard": 0,
        "Price": {
          "ChargeUnit": "HOUR",
          "UnitPrice": 0.26
        },
        "Status": "SELL",
        "TypeName": "Standard S3",
        "Zone": "ap-chongqing-1"
      }
    ],
    "RequestId": "2fba5b9c-e4ee-47ad-a776-dabb79ff2c35"
  }
}
```


## 5. Developer Resources

**It is recommended to use [`API 3.0 Explorer`](https://console.cloud.tencent.com/api/explorer). This tool provides various capabilities such as online debugging, signature verification, SDK code generation and quick API retrieval that significantly reduce the difficulty of using cloud APIs.**

Cloud API 3.0 comes with a set of complementary development tools that make it easier to call the API.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)
* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to this API are listed below. For other error codes, see [Common Error Codes](/document/api/599/15885#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidFilter | The specified filter is not supported. |
| InvalidParameterValue | Invalid parameter value. |
| InvalidParameterValue.LimitExceeded | The number of Filter parameter values exceeds the limit. |
| InvalidParameterValue.UnsupportedBatchInstanceChargeType | Model billing type not supported by Batch. |
| InvalidZone.MismatchRegion | The specified zone does not exist. |


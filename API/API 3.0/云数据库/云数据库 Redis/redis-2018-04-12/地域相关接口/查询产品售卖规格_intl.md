## 1. API Description

API domain name: redis.tencentcloudapi.com.

This API queries the capacity specifications of Redis instances in the specified availability zone and instance type. If you are not in the whitelist for the availability zone or type, you cannot view the details of the capacity specifications. You can submit a ticket to apply for listing in the desired whitelist

Default API request rate limit: 20 requests/sec.

Note: This API supports financial availability zones. As financial availability zones and non-financial availability zones are isolated, if the common parameter Region specifies a financial availability zone (e.g., ap-shanghai-fsi), it is necessary to specify a domain name with the financial availability zone too, preferably in the same region as specified in Region, such as redis.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/239/20005).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeProductInfo |
| Version | Yes | String | Common parameter; the value for this API: 2018-04-12 |
| Region | Yes | String | Common parameters; for details, see the [List of Regions](/document/api/239/20005#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| RegionSet | Array of [RegionConf](/document/api/239/20022#RegionConf) | Region-specific sale information |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided during troubleshooting. |

## 4. Sample

### Sample 1. Request Example

#### Input Sample Code

```
https://redis.tencentcloudapi.com/?Action=DescribeProductInfo
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "RegionSet": [
      {
        "RegionId": "ap-guangzhou",
        "RegionName": "Guangzhou",
        "RegionShortName": "GZ",
        "Area": "South China",
        "ZoneSet": [
          {
            "ZoneId": "ap-guangzhou-2",
            "ZoneName": "Guangzhou Zone 2",
            "IsSaleout": false,
            "IsDefault": false,
            "NetWorkType": [
              "basenet",
              "vpcnet"
            ],
            "ProductSet": [
              {
                "Type": 7,
                "TypeName": "Redis cluster edition",
                "MinBuyNum": 1,
                "MaxBuyNum": 10,
                "Saleout": false,
                "Engine": "Redis community edition",
                "Version": "Redis 4.0",
                "TotalSize": [
                  "12",
                  "20",
                  "32",
                  "64",
                  "96",
                  "128",
                  "256",
                  "384",
                  "512",
                  "768",
                  "1024",
                  "2048",
                  "3072",
                  "4096"
                ],
                "ShardSize": [
                  "4",
                  "8",
                  "12",
                  "16",
                  "20",
                  "24",
                  "32"
                ],
                "ReplicaNum": [
                  "1",
                  "2",
                  "3",
                  "4",
                  "5"
                ],
                "ShardNum": [
                  "3",
                  "5",
                  "8",
                  "12",
                  "16",
                  "24",
                  "32",
                  "40",
                  "48",
                  "64",
                  "80",
                  "96",
                  "128"
                ],
                "PayMode": "1",
                "EnableRepicaReadOnly": true
              },
              {
                "Type": 4,
                "TypeName": "CKV cluster edition",
                "MinBuyNum": 1,
                "MaxBuyNum": 10,
                "Saleout": false,
                "Engine": "Tencent Cloud CKV",
                "Version": "Redis 3.2",
                "TotalSize": [
                  "12",
                  "20",
                  "32",
                  "64",
                  "96",
                  "128",
                  "256",
                  "384",
                  "512",
                  "768",
                  "1024",
                  "2048",
                  "3072",
                  "4096"
                ],
                "ShardSize": [
                  "4",
                  "8",
                  "16",
                  "24",
                  "32",
                  "48",
                  "64",
                  "80",
                  "96",
                  "128",
                  "160",
                  "192",
                  "256",
                  "320",
                  "384"
                ],
                "ReplicaNum": [
                  "1",
                  "2",
                  "3",
                  "4",
                  "5"
                ],
                "ShardNum": [
                  "3",
                  "5",
                  "8",
                  "12",
                  "16",
                  "24",
                  "32",
                  "40",
                  "48",
                  "64",
                  "80",
                  "96",
                  "128"
                ],
                "PayMode": "1",
                "EnableRepicaReadOnly": false
              },
              {
                "Type": 2,
                "TypeName": "Redis master-slave edition",
                "MinBuyNum": 1,
                "MaxBuyNum": 10,
                "Saleout": false,
                "Engine": "Redis community edition",
                "Version": "Redis 2.8",
                "TotalSize": [
                  "1",
                  "2",
                  "4",
                  "8",
                  "12",
                  "16",
                  "20",
                  "24",
                  "32",
                  "40",
                  "48",
                  "60",
                  "0.25"
                ],
                "ShardSize": [
                  "1",
                  "2",
                  "4",
                  "8",
                  "12",
                  "16",
                  "20",
                  "24",
                  "32",
                  "40",
                  "48",
                  "60",
                  "0.25"
                ],
                "ReplicaNum": [
                  "1"
                ],
                "ShardNum": [
                  "1"
                ],
                "PayMode": "1",
                "EnableRepicaReadOnly": false
              },
              {
                "Type": 5,
                "TypeName": "Redis standalone edition",
                "MinBuyNum": 1,
                "MaxBuyNum": 10,
                "Saleout": false,
                "Engine": "Redis community edition",
                "Version": "Redis 2.8",
                "TotalSize": [
                  "1",
                  "2",
                  "4",
                  "8",
                  "12",
                  "16",
                  "20",
                  "24",
                  "32",
                  "40",
                  "48",
                  "60"
                ],
                "ShardSize": [
                  "1",
                  "2",
                  "4",
                  "8",
                  "12",
                  "16",
                  "20",
                  "24",
                  "32",
                  "40",
                  "48",
                  "60"
                ],
                "ReplicaNum": [
                  "0"
                ],
                "ShardNum": [
                  "1"
                ],
                "PayMode": "1",
                "EnableRepicaReadOnly": false
              },
              {
                "Type": 2,
                "TypeName": "Redis master-slave edition",
                "MinBuyNum": 1,
                "MaxBuyNum": 10,
                "Saleout": false,
                "Engine": "Redis community edition",
                "Version": "Redis 2.8",
                "TotalSize": [
                  "1",
                  "2",
                  "4",
                  "8",
                  "12",
                  "16",
                  "20",
                  "24",
                  "32",
                  "40",
                  "48",
                  "60"
                ],
                "ShardSize": [
                  "1",
                  "2",
                  "4",
                  "8",
                  "12",
                  "16",
                  "20",
                  "24",
                  "32",
                  "40",
                  "48",
                  "60"
                ],
                "ReplicaNum": [
                  "1"
                ],
                "ShardNum": [
                  "1"
                ],
                "PayMode": "0",
                "EnableRepicaReadOnly": false
              },
              {
                "Type": 3,
                "TypeName": "CKV standalone edition",
                "MinBuyNum": 1,
                "MaxBuyNum": 10,
                "Saleout": false,
                "Engine": "Tencent Cloud CKV",
                "Version": "Redis 3.2",
                "TotalSize": [
                  "4",
                  "8",
                  "16",
                  "24",
                  "32",
                  "48",
                  "64",
                  "80",
                  "96",
                  "128",
                  "160",
                  "192",
                  "256",
                  "320",
                  "384"
                ],
                "ShardSize": [
                  "4",
                  "8",
                  "16",
                  "24",
                  "32",
                  "48",
                  "64",
                  "80",
                  "96",
                  "128",
                  "160",
                  "192",
                  "256",
                  "320",
                  "384"
                ],
                "ReplicaNum": [
                  "0"
                ],
                "ShardNum": [
                  "1"
                ],
                "PayMode": "1",
                "EnableRepicaReadOnly": false
              }
            ]
          }
        ]
      }
    ],
    "RequestId": "3c5730c6-02f2-46fd-8bf1-725b8b608fb9"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=redis&Version=2018-04-12&Action=DescribeProductInfo)

### SDK

TencentCloud API 3.0 comes with a set of complementary development toolkits (SDKs) that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

Only the error codes related to the API business logic are listed below. For other error codes, see [Common Error Codes](/document/api/239/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| FailedOperation.SystemError | Internal system error, irrelevant to the business. |
| InvalidParameter | Parameter error |
| InvalidParameter.EmptyParam | Parameter is empty. |
| InvalidParameter.PermissionDenied | The API has no CAM permissions. |

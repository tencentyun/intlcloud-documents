## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (DescribeDiskConfigQuota) is used to query the cloud disk quota.

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeDiskConfigQuota |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InquiryType | Yes | String | Query type. Value range: <br><li>INQUIRY_CBS_CONFIG: query the configuration list of cloud disks <br><li>INQUIRY_CVM_CONFIG: query the configuration list of cloud disks and instances |
| Zones.N | No | Array of String | Queries the configurations in one or more [availability zones](/document/product/213/15753#ZoneInfo). |
| DiskChargeType | No | String | Billing method. Value range: <br><li>PREPAID: Prepaid <br><li>POSTPAID_BY_HOUR: Postpaid (pay as you go) |
| DiskTypes.N | No | String | Type of disk medium. Value range: <br><li>CLOUD_BASIC: HDD cloud storage<br><li>CLOUD_PREMIUM: Premium cloud storage <br><li>CLOUD_SSD: SSD cloud storage. |
| DiskUsage | No | String | The system disk or data disk. Value range: <br><li>SYSTEM_DISK: System disk <br><li>DATA_DISK: Data disk |
| InstanceFamilies.N | No | Array of String | Filter by the instance models, such as S1, I1 and M1. For more information, please see [Instance Types](https://cloud.tencent.com/document/product/213/11518) |
| CPU | No | Integer | Number of CPU cores in the instance |
| Memory | No | Integer | Memory size of the instance |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DiskConfigSet | Array of [DiskConfig](/document/api/362/15669#DiskConfig) | Configuration list of the cloud disk. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Querying Cloud Disk Configurations in Guangzhou Zone 2

Query the availability and specifications of cloud disks in the specified availability zone. In the returned response, if `Available` is `true`, the cloud disk is available for purchase, if it’s `false`, the cloud disks with the corresponding specifications is out of stock in the specified AZ. 

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=DescribeDiskConfigQuota
&InquiryType=INQUIRY_CBS_CONFIG
&Zones.0=ap-guangzhou-2
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "DiskConfigSet": [
      {
        "Available": true,
        "DiskChargeType": "POSTPAID_BY_HOUR",
        "Zone": "ap-guangzhou-2",
        "InstanceFamily": null,
        "DiskType": "CLOUD_BASIC",
        "DeviceClass": null,
        "DiskUsage": "DATA_DISK",
        "MinDiskSize": 10,
        "MaxDiskSize": 4000
      },
      {
        "Available": true,
        "DiskChargeType": "POSTPAID_BY_HOUR",
        "Zone": "ap-guangzhou-2",
        "InstanceFamily": null,
        "DiskType": "CLOUD_PREMIUM",
        "DeviceClass": null,
        "DiskUsage": "DATA_DISK",
        "MinDiskSize": 50,
        "MaxDiskSize": 4000
      },
      {
        "Available": false,
        "DiskChargeType": "POSTPAID_BY_HOUR",
        "Zone": "ap-guangzhou-2",
        "InstanceFamily": null,
        "DiskType": "CLOUD_SSD",
        "DeviceClass": null,
        "DiskUsage": "DATA_DISK",
        "MinDiskSize": 100,
        "MaxDiskSize": 4000
      }
    ],
    "RequestId": "55db49cf-b9d7-da27-825b-5a02ba6814b2"
  }
}
```

### Sample 2. Querying Available Cloud Disk Configurations for S3 Model in Guangzhou Zone 2

Query the cloud disk configurations that work with various instance models. In the returned values, when `Available` is `true`, the cloud disk is available for purchase. When `Available` is `false`, the cloud disks with the corresponding specifications have already been sold out.

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=DescribeDiskConfigQuota
&InquiryType=INQUIRY_CVM_CONFIG
&Zones.0=ap-guangzhou-2
&InstanceFamilies.0=S3
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "DiskConfigSet": [
      {
        "Available": true,
        "MaxDiskSize": 16000,
        "Zone": "ap-guangzhou-2",
        "InstanceFamily": "S3",
        "DiskType": "CLOUD_BASIC",
        "DeviceClass": "VSELF_3",
        "DiskUsage": "DATA_DISK",
        "MinDiskSize": 10,
        "DiskChargeType": "POSTPAID_BY_HOUR"
      },
      {
        "Available": true,
        "MaxDiskSize": 500,
        "Zone": "ap-guangzhou-2",
        "InstanceFamily": "S3",
        "DiskType": "CLOUD_BASIC",
        "DeviceClass": "VSELF_3",
        "DiskUsage": "SYSTEM_DISK",
        "MinDiskSize": 50,
        "DiskChargeType": "POSTPAID_BY_HOUR"
      },
      {
        "Available": true,
        "MaxDiskSize": 16000,
        "Zone": "ap-guangzhou-2",
        "InstanceFamily": "S3",
        "DiskType": "CLOUD_SSD",
        "DeviceClass": "VSELF_3",
        "DiskUsage": "DATA_DISK",
        "MinDiskSize": 100,
        "DiskChargeType": "POSTPAID_BY_HOUR"
      },
      {
        "Available": true,
        "MaxDiskSize": 500,
        "Zone": "ap-guangzhou-2",
        "InstanceFamily": "S3",
        "DiskType": "CLOUD_SSD",
        "DeviceClass": "VSELF_3",
        "DiskUsage": "SYSTEM_DISK",
        "MinDiskSize": 50,
        "DiskChargeType": "POSTPAID_BY_HOUR"
      }
    ],
    "RequestId": "55db49cf-b9d7-da27-825b-5a02ba6814b2"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=DescribeDiskConfigQuota)

### SDK

TencentCloud API 3.0 comes with SDKs that support multiple programming languages and make it easier to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following only lists the error codes related to this API. For other error codes, see [Common Error Codes](/document/api/362/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |

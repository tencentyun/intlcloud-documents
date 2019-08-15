## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (DescribeDiskOperationLogs) is used to query a list of cloud disk operation logs.

You can filter cloud disks by their IDs in the format of disk-a1kmcp13.


Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeDiskOperationLogs |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Filters.N | Yes | Array of [Filter](/document/api/362/15669#Filter) | Filter conditions. The following filter conditions are supported: <br/><li>disk-id - Array of String - Required or not: Yes - Filtered according to the cloud disk ID. Each request can specify up to 10 cloud disk IDs. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| DiskOperationLogSet | Array of [DiskOperationLog](/document/api/362/15669#DiskOperationLog) | The operation log list of the cloud disk.|
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Querying the Cloud Disk Operation Log List

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=DescribeDiskOperationLogs
&Filters.0.Name=disk-id
&Filters.0.Values.0=disk-ou4acu4i
&<Common request parameters>
```

#### Output Sample Code

```
{
  "DiskOperationLogSet": [
    {
      "OperationState": "SUCCESS",
      "StartTime": "2018-09-19 20:40:20",
      "Operator": "100004375281",
      "Operation": "CBS_OPERATION_MODIFY",
      "EndTime": "2018-09-19 20:40:20",
      "DiskId": "disk-ou4acu4i"
    },
    {
      "OperationState": "SUCCESS",
      "StartTime": "2018-09-19 20:40:16",
      "Operator": "100004375281",
      "Operation": "CBS_OPERATION_MODIFY",
      "EndTime": "2018-09-19 20:40:16",
      "DiskId": "disk-ou4acu4i"
    },
    {
      "OperationState": "SUCCESS",
      "StartTime": "2018-09-19 20:40:13",
      "Operator": "100004375281",
      "Operation": "CBS_OPERATION_EXPAND",
      "EndTime": "2018-09-19 20:40:13",
      "DiskId": "disk-ou4acu4i"
    },
    {
      "OperationState": "SUCCESS",
      "StartTime": "2018-09-19 20:39:59",
      "Operator": "100004375281",
      "Operation": "CBS_OPERATION_CREATE",
      "EndTime": "2018-09-19 20:39:59",
      "DiskId": "disk-ou4acu4i"
    }
  ]
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=DescribeDiskOperationLogs)

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
| InternalError.ComponentError | The request failed because of a dependent component. Please submit a ticket to resolve the issue. |
| InvalidDiskId.NotFound | The `DiskId` does not exist. |
| InvalidParameter | Invalid parameter |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| InvalidParameterValue.LimitExceeded | The number of parameter values exceeds the limit. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |

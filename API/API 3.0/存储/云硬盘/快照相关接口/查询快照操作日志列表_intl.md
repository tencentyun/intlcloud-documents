## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (DescribeSnapshotOperationLogs) is used to query a list of snapshot operation logs.

You can filter logs according to the snapshot ID. The snapshot ID format is as follows: snap-a1kmcp13.


Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeSnapshotOperationLogs |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| Filters.N | Yes | Array of [Filter](/document/api/362/15669#Filter) | Filter conditions. <br/><li>snapshot-id - Array of String - Required or not: Yes - Filtered according to the snapshot ID. Each request can specify up to 10 snapshot IDs. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| SnapshotOperationLogSet | Array of [SnapshotOperationLog](/document/api/362/15669#SnapshotOperationLog) | The snapshot operation log list. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1 Querying the Snapshot Operation Log List

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=DescribeSnapshotOperationLogs
&Filters.0.Name=snapshot-id
&Filters.0.Values.0=snap-0y61iiyj
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "SnapshotOperationLogSet": [
      {
        "OperationState": "SUCCESS",
        "StartTime": "2018-12-18 17:52:37",
        "Operator": "546816713",
        "SnapshotId": "snap-0y61iiyj",
        "Operation": "SNAP_OPERATION_ROLLBACK",
        "EndTime": "2018-12-18 17:52:38"
      },
      {
        "OperationState": "SUCCESS",
        "StartTime": "2018-12-18 17:51:47",
        "Operator": "546816713",
        "SnapshotId": "snap-0y61iiyj",
        "Operation": "SNAP_OPERATION_ROLLBACK",
        "EndTime": "2018-12-18 17:51:48"
      },
      {
        "OperationState": "SUCCESS",
        "StartTime": "2018-12-18 11:57:46",
        "Operator": "",
        "SnapshotId": "snap-0y61iiyj",
        "Operation": "ASP_OPERATION_CREATE_SNAP",
        "EndTime": "2018-12-18 11:57:47"
      }
    ],
    "RequestId": "0dc7b07a-5f6b-46c4-b1d9-048e37d1c33c"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=DescribeSnapshotOperationLogs)

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
| InvalidParameter | Invalid parameter |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| InvalidParameterValue.LimitExceeded | The number of parameter values exceeds the limit. |
| InvalidSnapshotId.NotFound | The `SnapshotId` does not exist. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |

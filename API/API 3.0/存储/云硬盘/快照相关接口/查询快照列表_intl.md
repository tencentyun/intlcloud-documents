## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (DescribeSnapshots) is used to query the details of snapshots.

* Filter the results by the snapshot ID, the ID of cloud disk, and the type of cloud disk. The relationship between different conditions is AND. For more information about filtering, please see `Filter`.
* If the parameter is empty, a certain number (specified by `Limit`; the default is 20) of snapshots in the current account are returned.

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value ​used for this API: DescribeSnapshots |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| SnapshotIds.N | No | Array of String | List of IDs of the snapshots to be query. This parameter does not support specifying both `SnapshotIds` and `Filters`. |
| Filters.N | No | Array of [Filter](/document/api/362/15669#Filter) | Filter conditions. The specification of both the `SnapshotIds` and `Filters` parameters is not supported. <br><li>snapshot-id - Array of String - Required or not: No - (Filter condition) Filter by the snapshot ID. The format of the snapshot ID is as follows: `snap-11112222`. <br><li>snapshot-name - Array of String - Required or not: No - (Filter condition) Filter by the snapshot name. <br><li>snapshot-state - Array of String - Required or not: No - (Filter condition) Filter by the snapshot status (NORMAL: normal &#124; CREATING: creating &#124; ROLLBACKING: rolling back). <br><li>disk-usage - Array of String - Required or not: No - (Filter condition) Filter by the type of the cloud disk for which the snapshot is created (SYSTEM_DISK: system disk &#124; DATA_DISK: data disk). <br><li>project-id - Array of String - Required or not: No - (Filter condition) Filter by ID of the project to which the cloud disk belongs. <br><li>disk-id - Array of String - Required or not: No - (Filter condition) Filter by the ID of the cloud disk for which the snapshot is created. <br><li>zone - Array of String - Required or not: No - (Filter condition) Filter by [Availability Zone](/document/product/213/15753#ZoneInfo). <br><li>encrypt - Array of String - Required or not: No - (Filter condition) According to whether it is an encrypted disk snapshot. (TRUE: indicates an encrypted disk snapshot &#124; FALSE: indicates that it is not an encrypted disk snapshot.) |
| Offset | No | Integer | Offset. Default is 0. For more information on `Offset`, please see relevant sections in API [Introduction](/document/product/362/15633). |
| Limit | No | Integer | Allowed number of results. Default is 20. Maximum is 100. For more information on `Limit`, please see relevant sections in API [Introduction](/document/product/362/15633). |
| Order | No | String | The order of the output cloud disk list. Value range: <br><li>ASC: Ascending order <br><li>DESC: Descending order |
| OrderField | No | String | The field by which the snapshot list is sorted. Value range: <br><li>CREATETIME: sorted by the creation time of the snapshots <br>By default, the snapshot list is sorted by the creation time of snapshots. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of snapshots. |
| SnapshotSet | Array of [Snapshot](/document/api/362/15669#Snapshot) | List of snapshot details. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1 Querying Snapshots with NORMAL Status in Guangzhou Zone 2

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=DescribeSnapshots
&Filters.0.Name=snapshot-state
&Filters.0.Values.0=NORMAL
&Filters.1.Name=zone
&Filters.1.Values.0=ap-guangzhou-2
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 1,
    "SnapshotSet": [
      {
        "Placement": {
          "ProjectId": 0,
          "Zone": "ap-guangzhou-2"
        },
        "IsPermanent": true,
        "DiskUsage": "DATA_DISK",
        "DeadlineTime": null,
        "Percent": 100,
        "DiskSize": 10,
        "DiskId": "disk-22rkwrvw",
        "SnapshotName": "test_snap_count",
        "SnapshotId": "snap-1i97mf6d",
        "Encrypt": false,
        "CreateTime": "2018-04-12 17:34:45",
        "SnapshotState": "NORMAL",
        "ImageCount": 1,
        "Images": [
          {
            "ImageId": "img-f805a134",
            "ImageName": "test-image"
          }
        ]
      }
    ],
    "RequestId": "3a823099-86f1-6887-6273-5a1f8043d8a3"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=DescribeSnapshots)

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
| InvalidFilter | The specified Filter is not supported. |
| InvalidParameterValue | Invalid parameter value. Parameter value is in an incorrect format or is not supported. |
| MissingParameter | Missing parameter. A required parameter is missing in the request. |

## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API action (DescribeAutoSnapshotPolicies) is used to query scheduled snapshot policies.

* You can query the detailed information of scheduled snapshot policies by ID, name, or status. Insert `AND` between different values. For details on filtering information, see `Filter`.
* If the parameter is empty, a certain number (specified by `Limit`; the default is 20) of the scheduled snapshot policy lists are returned to the current user.


Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeAutoSnapshotPolicies |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| AutoSnapshotPolicyIds.N | No | Array of String | List of the IDs of the scheduled snapshot policies to be queried. Specification of both the `AutoSnapshotPolicyIds` and `Filters` parameters is not supported. |
| Filters.N | No | Array of [Filter](/document/api/362/15669#Filter) | Filter conditions. `AutoSnapshotPolicyIds` and `Filters` parameters cannot be specified at the same time.<br><li>auto-snapshot-policy-id - Array of String - Required or not: No - (Filter condition) Filters according to the scheduled snapshot policy ID. The format of the scheduled snapshot policy ID is as follows: `asp-11112222`. <br><li>auto-snapshot-policy-state - Array of String - Required or not: No - (Filter condition) Filters according to the status of the scheduled snapshot policy. The format of the scheduled snapshot policy ID is as follows: `asp-11112222`. (NORMAL: normaI | ISOLATED: isolated)<br><li>auto-snapshot-policy-name - Array of String - Required or not: No - (Filter condition) Filters according to the name of the scheduled snapshot policy. |
| Limit | No | Integer | Allowed number of results. Default is 20. Maximum is 100. For more information on `Limit`, see the relevant sections in API [Introduction](/document/362/13158). |
| Offset | No | Integer | Offset. Default is 0. For more information on `Offset`, see the relevant sections in API [Introduction](/document/362/13158). |
| Order | No | String | Outputs the ordering of the scheduled snapshot lists. Value range: <br><li>ASC: Ascending order <br><li>DESC: Descending order |
| OrderField | No | String | The field by which the scheduled snapshot list is sorted. Value range: <br><li>CREATETIME: sorted by the creation time of the scheduled snapshots <br>By default, the snapshot list is sorted by the creation time of snapshots. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | The number of scheduled snapshot policies in effect. |
| AutoSnapshotPolicySet | Array of [AutoSnapshotPolicy](/document/api/362/15669#AutoSnapshotPolicy) | The list of scheduled snapshot policies. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1 Querying scheduled snapshot Policies with NORMAL Status

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=DescribeAutoSnapshotPolicies
&Filters.0.Name=auto-snapshot-policy-state
&Filters.0.Values.0=NORMAL
&Limit=3
&Offset=0
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "AutoSnapshotPolicySet": [
      {
        "DiskIdSet": [],
        "IsActivated": 1,
        "AutoSnapshotPolicyState": "NORMAL",
        "AutoSnapshotPolicyName": "SnapshotPolicy1",
        "IsPermanent": 0,
        "NextTriggerTime": "2017-12-04 12:00:00",
        "AutoSnapshotPolicyId": "asp-lfp6fi4f",
        "Policy": [
          {
            "DayOfWeek": [
              1,
              4
            ],
            "Hour": [
              12
            ]
          }
        ],
        "CreateTime": "2017-11-01 10:46:22",
        "RetentionDays": 7
      },
      {
        "DiskIdSet": [],
        "IsActivated": 1,
        "AutoSnapshotPolicyState": "NORMAL",
        "AutoSnapshotPolicyName": "SnapshotPolicy2”",
        "IsPermanent": 0,
        "NextTriggerTime": "2017-12-03 10:00:00",
        "AutoSnapshotPolicyId": "asp-nqu08k2l",
        "Policy": [
          {
            "DayOfWeek": [
              0
            ],
            "Hour": [
              10
            ]
          }
        ],
        "CreateTime": "2017-11-17 15:01:25",
        "RetentionDays": 7
      }
    ],
    "TotalCount": 2,
    "RequestId": "701c8a35-ed66-fc79-3795-5a1fa72cdbf1"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=DescribeAutoSnapshotPolicies)

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

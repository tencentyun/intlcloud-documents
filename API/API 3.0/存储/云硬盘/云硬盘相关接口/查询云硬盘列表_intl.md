## 1. API Description

Domain name for API request: cbs.tencentcloudapi.com.

This API (DescribeDisks) is used to query the list of cloud disks.

* You can query the details of one or more cloud disks by ID, type or status. The relationship between different conditions is AND. For more information about filtering, please see `Filter`.
* If the parameter is empty, a certain number (specified by `Limit`; the default is 20) of cloud disk lists are returned to the current user.

Default request rate limit: 20/sec.

Note: This API supports finance AZs. As finance AZs and non-finance AZs are isolated, when accessing the services in a finance AZ (with the common parameter Region specifying a financial availability zone), it is necessary to specify a domain name with the finance AZ, preferably in the same region as specified in Region.



## 2. Input Parameters

The list below contains only the API request parameters and certain common parameters. For the complete common parameter list, see [Common Request Parameters](/document/api/362/15637).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The value used for this API: DescribeDisks |
| Version | Yes | String | Common parameter. The value used for this API: 2017-03-12 |
| Region | Yes | String | Common parameter. For more information, see [List of Regions](/document/api/362/15637#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| DiskIds.N | No | Array of String | Query by one or more cloud disk IDs, such as `disk-11112222`. For the format of this parameter, please see the ids.N section of the API [Introduction](/document/product/362/15633). This parameter does not support specifying both `DiskIds` and `Filters`. |
| Filters.N | No | Array of [Filter](/document/api/362/15669#Filter) | Filter conditions. This parameter does not support specifying both `DiskIds` and `Filters`. <br><li>disk-usage - Array of String - Required or not: No - (Filter condition) Filter by the cloud disk type. (SYSTEM_DISK: system disk &#124; DATA_DISK: data disk) <br><li>disk-charge-type - Array of String - Required or not: No - (Filter condition) Filter by the billing method of the cloud disk. (PREPAID: prepaid &#124; POSTPAID_BY_HOUR: postpaid) <br><li>portable - Array of String- Required or not: No - (Filter condition) Filter according to whether they are elastic cloud disks or not. (TRUE: elastic cloud disk &#124; FALSE: non-elastic cloud disk) <br><li>project-id - Array of Integer - Required or not: No - (Filter condition) Filter by the ID of the project to which the cloud disk belongs. <br><li>disk-id - Array of String - Required or not: No - (Filter condition) Filter by the cloud disk ID, such as `disk-11112222`. <br><li>disk-name - Array of String - Required or not: No - (Filter condition) Filter by cloud disk name. <br><li>disk-type - Array of String - Required or not: No - (Filter condition) Filter by the type of the cloud disk medium (CLOUD_BASIC: HDD cloud disk &#124; CLOUD_PREMIUM: premium cloud disk &#124; CLOUD_SSD: SSD cloud disk.) <br><li>disk-state - Array of String - Required or not: No - (Filter condition) Filter by the cloud disk status. (UNATTACHED: unmounted &#124; ATTACHING: mounting &#124; ATTACHED: mounted &#124; DETACHING: unmounting &#124; EXPANDING: expanding capacity &#124; ROLLBACKING: rolling back &#124; TORECYCLE: to be reclaimed.) <br><li>instance-id - Array of String - Required or not: No - (Filter condition) Filter by the ID of the CVM instance to which the cloud disk is mounted. You can use this parameter to query the cloud disk mounted on the specified CVM. <br><li>zone - Array of String - Required or not: No - (Filter condition) Filter by the [availability zone](/document/product/213/15753#ZoneInfo) <br><li>instance-ip-address - Array of String - Required or not: No - (Filter condition) Filter by the IP address of the private or public network of the CVM to which the cloud disk is mounted. <br><li>instance-name - Array of String - Required or not: No - (Filter condition) Filter by the name of the instance to which the cloud disk is mounted. <br><li>tag-key - Array of String - Required or not: No - (Filter condition) Filter by the tag key. <br><li>tag-value - Array of String - Required or not: No - (Filter condition) Filter by the tag value. <br><li>tag:tag-key - Array of String - Required or not: No - (Filter condition) Filter by the tag key value pair. Replace `tag-key` with your actual tag key.|
| Offset | No | Integer | Offset. Default is 0. For more information on `Offset`, please see relevant sections in API [Introduction](/document/product/362/15633). |
| Limit | No | Integer | Allowed number of results. Default is 20. Maximum is 100. For more information on `Limit`, please see relevant sections in API [Introduction](/document/product/362/15633). |
| Order | No | String |Indicates the sorting order of the output cloud disk list. Value range: <br><li>ASC: Ascending order <br><li>DESC: Descending order |
| OrderField | No | String | The field by which the cloud disk list is sorted. Value range: <br><li>CREATE_TIME: sorted by the creation time of cloud disks <br><li>DEADLINE: sorted by the expiration time of cloud disks <br>The default value is CREATE_TIME. |
| ReturnBindAutoSnapshotPolicy | No | Boolean | Whether to return the ID of the scheduled snapshot policy bound to the cloud disk in the cloud disk details. TRUE: return; FALSE: do not return. |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of cloud disks that meet the condition. |
| DiskSet | Array of [Disk](/document/api/362/15669#Disk) | List of cloud disk details. |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Querying All the Mounted Data Disks

#### Input Sample Code

```
https://cbs.tencentcloudapi.com/?Action=DescribeDisks
&Filters.0.Name=disk-usage
&Filters.0.Values.0=DATA_DISK
&Filters.1.Name=disk-state
&Filters.1.Values.0=ATTACHED
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 1,
    "RequestId": "e2386a23-48c1-4c18-9a36-4e7354f333b2",
    "DiskSet": [
      {
        "DeleteWithInstance": false,
        "Encrypt": false,
        "DiskType": "CLOUD_BASIC",
        "AutoRenewFlagError": false,
        "Rollbacking": false,
        "RenewFlag": "NOTIFY_AND_MANUAL_RENEW",
        "DiskName": "test",
        "Tags": [],
        "InstanceId": "",
        "DifferDaysOfDeadline": 1,
        "DiskId": "disk-b94t5dzt",
        "DiskState": "ATTACHED",
        "Placement": {
          "ProjectId": 0,
          "Zone": "ap-guangzhou-2"
        },
        "IsReturnable": false,
        "DeadlineTime": "2018-10-26 10:55:43",
        "Attached": true,
        "DiskSize": 10,
        "DiskUsage": "DATA_DISK",
        "Portable": true,
        "DiskChargeType": "PREPAID",
        "SnapshotAbility": true,
        "DeadlineError": false,
        "RollbackPercent": 100,
        "AutoSnapshotPolicyIds": null,
        "ReturnFailCode": 3,
        "CreateTime": "2018-09-26 17:36:07"
      }
    ]
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=cbs&Version=2017-03-12&Action=DescribeDisks)

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

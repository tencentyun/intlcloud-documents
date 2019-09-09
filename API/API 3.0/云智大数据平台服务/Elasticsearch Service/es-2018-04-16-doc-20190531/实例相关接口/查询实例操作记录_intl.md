## 1. API Description

API domain name: es.tencentcloudapi.com.

This API queries the activity records for the specified instance by the specified criteria.

Default API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if a financial region, such as ap-shanghai-fsi, is assigned to the common parameter Region, we recommend you include that financial region in your domain name  , such as es.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/845/30623).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeInstanceOperations |
| Version | Yes | String | Common parameter. The version of this API: 2018-04-16 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/845/30623#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| InstanceId | Yes | String | Cluster instance ID |
| StartTime | Yes | String | Start time, such as "2019-03-07 16:30:39" |
| EndTime | Yes | String | End time, such as "2019-03-30 20:18:03" |
| Offset | Yes | Integer | Pagination start value |
| Limit | Yes | Integer | Number of entries per page |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of activities |
| Operations | Array of [Operation](/document/api/845/30634#Operation) | Activity record |
| RequestId | String | The unique ID of a request, which is required for each troubleshooting case. |

## 4. Examples

### Example 1. Querying the Activity Record of an ES Cluster Instance

#### Input Sample Code

```
https://es.tencentcloudapi.com/?Action=DescribeInstanceOperations
&InstanceId=es-f5mwm28u
&StartTime=2019-01-30 20:18:03
&EndTime=2019-03-30 20:18:03
&Offset=0
&Limit=30
&<Common request parameter>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 1,
    "Operations": [
      {
        "Id": 6173,
        "StartTime": "2019-03-07 16:30:39",
        "Type": "CreateInstance",
        "Detail": {
          "OldInfo": [],
          "NewInfo": []
        },
        "Result": "completed",
        "Tasks": [
          {
            "Name": "prepareResource",
            "Progress": 1,
            "FinishTime": "2019-03-07 16:31:11",
            "SubTasks": []
          },
          {
            "Name": "deployESCluster",
            "Progress": 1,
            "FinishTime": "2019-03-07 16:34:32",
            "SubTasks": []
          },
          {
            "Name": "deployKibana",
            "Progress": 1,
            "FinishTime": "2019-03-07 16:35:13",
            "SubTasks": []
          },
          {
            "Name": "configLB",
            "Progress": 1,
            "FinishTime": "2019-03-07 16:35:15",
            "SubTasks": []
          }
        ],
        "Progress": 1
      }
    ],
    "RequestId": "870dd618-b1ae-40cc-a5a9-22b867367ed7"
  }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=es&Version=2018-04-16&Action=DescribeInstanceOperations)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/845/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InvalidParameter | Incorrect parameter. |
| ResourceInUse | Resource is occupied. |

## **1. API Description**
API request domain name: batch.tencentcloudapi.com.

Used to query compute environment details

Default API request frequency limit: 2 times/second.



## **2. Input Parameters**

The following list of request parameters lists only the API request parameters and some common parameters. For the complete list of common parameters, see [Common Request Parameters](/document/api/599/15883).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the value for this API: DescribeComputeEnv |
| Version | Yes | String | Common parameter; the value for this API: 2017-03-12 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/599/15883#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product. |
| EnvId | Yes | String | Compute environment ID |

## **3. Output Parameters**

| Parameter name | Type | Description |
|---------|---------|---------|
| EnvId | String | Compute environment ID |
| EnvName | String | Compute environment name |
| Placement | [Placement](/document/api/599/15912#Placement) | Location information |
| CreateTime | String | Compute environment creation time |
| ComputeNodeSet | Array of [ComputeNode](/document/api/599/15912#ComputeNode) | List of compute node information |
| ComputeNodeMetrics | [ComputeNodeMetrics](/document/api/599/15912#ComputeNodeMetrics) | Compute node statistical metrics |
| DesiredComputeNodeCount | Integer | Number of desired compute nodes |
| EnvType | String | Compute environment type |
| RequestId | String | The unique request ID which is returned for each request. The RequestId for the current request needs to be provided when troubleshooting. |

## 4. Examples

### Example 1. Viewing Compute Environment Details

#### Input

```
https://batch.tencentcloudapi.com/?Action=DescribeComputeEnv
&EnvId=env-lcpcej85
&<Common request parameter>
```

#### Output

```
{
  "Response": {
    "ComputeNodeMetrics": {
      "AbnormalCount": 1,
      "CreatedCount": 0,
      "CreatingCount": 0,
      "CreationFailedCount": 0,
      "DeletingCount": 0,
      "RunningCount": 1,
      "SubmittedCount": 0
    },
    "ComputeNodeSet": [
      {
        "AgentVersion": "1.1.9",
        "ComputeNodeId": "node-noa8vefu",
        "ComputeNodeInstanceId": "ins-0kj3gz6s",
        "ComputeNodeState": "ABNORMAL",
        "Cpu": 1,
        "Mem": 2,
        "ResourceCreatedTime": "2018-03-08T11:49:17Z",
        "TaskInstanceNumAvailable": 1
      },
      {
        "AgentVersion": "1.1.9",
        "ComputeNodeId": "node-9yzd5jei",
        "ComputeNodeInstanceId": "ins-jyafz2sk",
        "ComputeNodeState": "RUNNING",
        "Cpu": 1,
        "Mem": 2,
        "ResourceCreatedTime": "2018-03-09T13:15:44Z",
        "TaskInstanceNumAvailable": 1
      }
    ],
    "CreateTime": "2018-03-08T11:48:43Z",
    "DesiredComputeNodeCount": 2,
    "EnvId": "env-lcpcej85",
    "EnvName": "test compute env",
    "EnvType": "MANAGED",
    "Placement": {
      "Zone": "ap-guangzhou-2"
    },
    "RequestId": "274cbd4f-77d2-4bf6-9984-643318ed3ef8"
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
| InvalidParameter.EnvIdMalformed | Invalid compute environment ID format. |
| ResourceNotFound.ComputeEnv | The specified compute environment does not exist. |


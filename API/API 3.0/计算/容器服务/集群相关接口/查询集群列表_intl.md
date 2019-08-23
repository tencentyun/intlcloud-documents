## 1. API Description

API domain name: tke.tencentcloudapi.com.

This API describes the cluster list.

API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if a financial region,such as ap-shanghai-fsi, is assigned to the common parameter `Region`, we recommend you include that financial region in your domain name , such as tke.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/457/31856).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: DescribeClusters |
| Version | Yes | String | Common parameter. The version of this API: 2018-05-25 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/457/31856#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product.
| ClusterIds.N | No | Array of String | List of cluster IDs (if this parameter is empty, <br/>all clusters under the account are obtained) |
| Offset | No | Integer | Offset; default is 0 |
| Limit | No | Integer | Maximum number of output entries; default is 20 |
| Filters.N | No | Array of [Filter](/document/api/457/31866#Filter) | Filter. Currently, only ClusterName is supported |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Total number of clusters |
| Clusters | Array of [Cluster](/document/api/457/31866#Cluster) | Cluster information list |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Querying the Cluster List

Describing a cluster list.

#### Input Sample Code

```
https://tke.tencentcloudapi.com/?Action=DescribeClusters
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "TotalCount": 1,
    "Clusters": [
      {
        "ClusterId": "cls-xxxxxxx",
        "ClusterName": "Cluster",
        "ClusterDescription": "",
        "ClusterVersion": "1.10.5",
        "ClusterOs": "ubuntu16.04.1 LTSx86_64",
        "ClusterType": "INDEPENDENT_CLUSTER",
        "ClusterNetworkSettings": {
          "ClusterCIDR": "10.211.0.0/16",
          "IgnoreClusterCIDRConflict": false,
          "MaxNodePodNum": 256,
          "MaxClusterServiceNum": 256,
          "Ipvs": false,
          "VpcId": "vpc-xxxxxx"
        },
        "ClusterNodeNum": 3
      }
    ],
    "RequestId": "a1be36f0-1aa4-4af2-a289-da021bcef89f"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=tke&Version=2018-05-25&Action=DescribeClusters)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### Command line tools

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes](/document/api/457/15694#.E5.85.AC.E5.85.B1.E9.94.99.E8.AF.AF.E7.A0.81).

| Error Code | Description |
|---------|---------|
| InternalError | Internal error. |
| InternalError.Db | Database error. |
| InternalError.DbAffectivedRows | Database effective function error. |
| InternalError.Param | Param. |
| InternalError.PublicClusterOpNotSupport | The cluster does not support the current operation. |
| InternalError.QuotaMaxClsLimit | Quota limit is exceeded. |
| InternalError.QuotaMaxNodLimit | Quota limit is exceeded. |
| InvalidParameter | Invalid parameter. |
| LimitExceeded | Quota limit is exceeded. |
| ResourceNotFound | Resource does not exist. |

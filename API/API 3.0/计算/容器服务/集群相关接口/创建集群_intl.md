## 1. API Description

API domain name: tke.tencentcloudapi.com.

This API creates a Cluster.

API request rate limit: 20 requests/sec.

Note: This API supports financial regions. As financial regions and non-financial regions are isolated, if a financial region, such as ap-shanghai-fsi, is assigned to the common parameter `Region`, we recommend you include that financial region in your domain name , such as tke.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/457/31856).

| Parameter Name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter. The name of this API: CreateCluster |
| Version | Yes | String | Common parameter. The version of this API: 2018-05-25 |
| Region | Yes | String | Common parameter. For more information, see the [list of regions](/document/api/457/31856#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8) supported by the product.
| ClusterCIDRSettings | Yes | [ClusterCIDRSettings](/document/api/457/31866#ClusterCIDRSettings) | Cluster container network configuration information |
| ClusterType | Yes | String | Cluster type. MANAGED_CLUSTER: managed cluster; INDEPENDENT_CLUSTER: independent cluster. |
| RunInstancesForNode.N | No | Array of [RunInstancesForNode](/document/api/457/31866#RunInstancesForNode) | Pass-through parameter for CVM instance creation, which is in the format of a JSON string. For more information, see the API for [creating a CVM instance](https://cloud.tencent.com/document/product/213/15730).
| ClusterBasicSettings | No | [ClusterBasicSettings](/document/api/457/31866#ClusterBasicSettings) | Basic configuration information of a cluster |
| ClusterAdvancedSettings | No | [ClusterAdvancedSettings](/document/api/457/31866#ClusterAdvancedSettings) | Advanced configuration information of a cluster |
| InstanceAdvancedSettings | No | [InstanceAdvancedSettings](/document/api/457/31866#InstanceAdvancedSettings) | Additional information need to be specified for the CVM instance |
| ExistedInstancesForNode.N | No | Array of [ExistedInstancesForNode](/document/api/457/31866#ExistedInstancesForNode) | Configuration information of existing instances |

## 3. Output Parameters

| Parameter Name | Type | Description |
|---------|---------|---------|
| ClusterId | String | Cluster ID |
| RequestId | String | Unique ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues.  |

## 4. Samples

### Sample 1. Creating a Managed Cluster

Create a managed cluster

#### Input Sample Code

```
https://tke.tencentcloudapi.com/?Action=CreateCluster
&ClusterType=MANAGED_CLUSTER
&ClusterCIDRSettings.ClusterCIDR=10.4.0.0/14
&RunInstancesForNode.0.NodeRole=WORKER
&RunInstancesForNode.0.RunInstancesPara.0={"VirtualPrivateCloud":{"SubnetId":"subnet-xxx","VpcId":"vpc-xxx"},"Placement":{"Zone":"ap-region-1","ProjectId":1032509},"InstanceType":"S3.LARGE8","SystemDisk":{"DiskType":"CLOUD_PREMIUM"},"DataDisks":[{"DiskType":"CLOUD_PREMIUM","DiskSize":50}],"InstanceCount":1,"InternetAccessible":{"PublicIpAssigned":true,"InternetMaxBandwidthOut":1},"LoginSettings":{"Password":"YourPassword"},"UserData":"IyEvYmluL3NoCgplY2hvIGFhYQo="}
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "ClusterId": "cls-xxx",
    "RequestId": "eac6b301-a322-493a-8e36-83b295459397"
  }
}
```

### Sample 2. Creating an Independent Cluster

Create an independent cluster

#### Input Sample Code

```
https://tke.tencentcloudapi.com/?Action=CreateCluster
&ClusterType=INDEPENDENT_CLUSTER
&ClusterCIDRSettings.ClusterCIDR=10.4.0.0/14
&RunInstancesForNode.0.NodeRole=MASTER_ETCD
&RunInstancesForNode.0.RunInstancesPara.0={"VirtualPrivateCloud":{"SubnetId":"subnet-xxx","VpcId":"vpc-xxx"},"Placement":{"Zone":"ap-region-1","ProjectId":1032509},"InstanceType":"S3.LARGE8","SystemDisk":{"DiskType":"CLOUD_PREMIUM"},"DataDisks":[{"DiskType":"CLOUD_PREMIUM","DiskSize":50}],"InstanceCount":3,"InternetAccessible":{"PublicIpAssigned":true,"InternetMaxBandwidthOut":1},"LoginSettings":{"Password":"YourPassword"},"UserData":"IyEvYmluL3NoCgplY2hvIGFhYQo="}
&RunInstancesForNode.1.NodeRole=WORKER
&RunInstancesForNode.1.RunInstancesPara.0={"VirtualPrivateCloud":{"SubnetId":"subnet-xxx","VpcId":"vpc-xxx"},"Placement":{"Zone":"ap-region-1","ProjectId":1032509},"InstanceType":"S3.LARGE8","SystemDisk":{"DiskType":"CLOUD_PREMIUM"},"DataDisks":[{"DiskType":"CLOUD_PREMIUM","DiskSize":50}],"InstanceCount":1,"InternetAccessible":{"PublicIpAssigned":true,"InternetMaxBandwidthOut":1},"LoginSettings":{"Password":"YourPassword"},"UserData":"IyEvYmluL3NoCgplY2hvIGFhYQo="}
&<Common request parameters>
```

#### Output Sample Code

```
{
  "Response": {
    "ClusterId": "cls-xxx",
    "RequestId": "eac6b301-a322-493a-8e36-83b295459397"
  }
}
```


## 5. Resources for Developers

### API Explorer

**This tool allows online call, signature authentication, SDK code generation and quick search of APIs to greatly improve the efficiency of using TencentCloud APIs.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=tke&Version=2018-05-25&Action=CreateCluster)

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
| InternalError.AccountUserNotAuthenticated | The account has not been authenticated. |
| InternalError.CidrConflictWithOtherCluster | The CIDR conflicts with a CIDR of another cluster. |
| InternalError.CidrConflictWithOtherRoute | The CIDR conflicts with another route. |
| InternalError.CidrConflictWithVpcCidr | The CIDR conflicts with the VPC. |
| InternalError.CidrConflictWithVpcGlobalRoute | The CIDR conflicts with the global route. |
| InternalError.CidrInvali | Invalid CIDR. |
| InternalError.CidrMaskSizeOutOfRange | Invalid CIDR mask. |
| InternalError.CreateMasterFailed | Cluster creation failed. |
| InternalError.CvmCommon | Error creating a node by CVM. |
| InternalError.Db | Database error. |
| InternalError.DbAffectivedRows | Database effective function error. |
| InternalError.InitMasterFailed | Master node initialization failed. |
| InternalError.InvalidPrivateNetworkCidr | Invalid CIDR. |
| InternalError.Param | Param. |
| InternalError.PublicClusterOpNotSupport | The cluster does not support the current operation. |
| InternalError.QuotaMaxClsLimit | Quota limit is exceeded. |
| InternalError.QuotaMaxNodLimit | Quota limit is exceeded. |
| InternalError.UnexceptedInternal | UnexceptedInternal. |
| InternalError.VpcCommon | VPC error. |
| InternalError.VpcRecodrNotFound | No VPC record found. |
| InvalidParameter | Invalid parameter. |
| LimitExceeded | Quota limit is exceeded. |

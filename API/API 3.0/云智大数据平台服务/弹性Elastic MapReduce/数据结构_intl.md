## COSSettings

COS-related Settings

Referenced by API: CreateInstance, DescribeInstances.

| Name | Type | Required | Description |
|------|------|----------|------|
| LogOnCosPath | String | Yes | COS path of the log |
| CosSecretId | String | Yes | COS SecretId |
| CosSecretKey | String | Yes | COS SecrectKey |

## ClusterInfoResult

Query result

Referenced by API: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| TotalCnt | Integer | Quantity <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| ClusterList | Array of [ClusterInstanceInfo](#ClusterInstanceInfo) | Cluster information list <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## ClusterInstanceInfo

Instance information

Referenced by API: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| ClusterId | String | clusterId |
| StatusDesc | String | Status description <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| ClusterName | String | Cluster name <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| ZoneId | Integer | Cluster region |
| AppId | Integer | User APPID |
| Addtime | String | Creation time <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| Runtime | String | Running duration <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| Config | [EMRProductConfigSettings](#EMRProductConfigSettings) | Cluster configuration <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| MasterIp | String | Cluster IP |
| EmrVersion | String | Cluster version |
| ChargeType | Integer | Cluster billing method |

## CreateInstanceResult

Return value of the creation API

Referenced by API: CreateInstance.

| Name | Type | Description |
|------|------|-------|
| ClientToken | String | Client token |
| InstanceName | String | Cluster name |
| DealNames | Array of String | Order list |

## EMRProductConfigSettings

config information of the cluster

Referenced by API: DescribeInstances.

| Name | Type | Description |
|------|------|-------|
| SoftInfo | Array of String | Cluster software information <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| MasterNodeSize | Integer | Number of master nodes <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| CoreNodeSize | Integer | Number of core nodes <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| TaskNodeSize | Integer | Number of task nodes <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| ComNodeSize | Integer | Number of common nodes <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| MasterResourceSpec | [NodeSpec](#NodeSpec) | Master node specification <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| CoreResourceSpec | [NodeSpec](#NodeSpec) | Core node specification <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| TaskResourceSpec | [NodeSpec](#NodeSpec) | Task node specification <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| CommonResourceSpec | [NodeSpec](#NodeSpec) | Common node specification <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| Oncos | Boolean | Whether to use COS <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| COSSettings | [COSSettings](#COSSettings) | COS configuration <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## InquiryPriceResult

Price inquiry output

Referenced by API: InquiryPriceCreateInstance, InquiryPriceScaleOutInstance.

| Name | Type | Description |
|------|------|-------|
| OriginalCost | Float | Original price |
| DiscountCost | Float | Discounted price |
| TimeUnit | String | Time unit |
| TimeSpan | Integer | Time span |

## LoginSettings

Login settings

Referenced by API: CreateInstance.

| Name | Type | Required | Description |
|------|------|----------|------|
| Password | String | No | Password |
| PublicKeyId | String | No | Public Key |

## MultiDisk

Multi-cloud disk parameters

Referenced by API: CreateInstance, DescribeInstances, InquiryPriceCreateInstance.

| Name | Type | Required | Description |
|------|------|----------|------|
| DiskType | String | Yes | Cloud disk type; value range: "CLOUD_PREMIUM", "CLOUD_SSD", or "CLOUD_BASIC" |
| Volume | Integer | Yes | Cloud disk size |

## NodeSpec

Node description

Referenced by API: CreateInstance, DescribeInstances, InquiryPriceCreateInstance.

| Name | Type | Required | Description |
|------|------|----------|------|
| Memory | Integer | Yes | Memory size in MB <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| CPUCores | Integer | Yes | Number of CPU cores <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| Volume | Integer | Yes | Data disk size <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| DiskType | String | Yes | Disk type <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| Spec | String | Yes | Node specification description <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| RootDiskVolume | Integer | Yes | System disk size <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| StorageType | Integer | Yes | Storage type <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| SpecName | String | No | Specification name <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| MultiDisks | Array of [MultiDisk](#MultiDisk) | No | Multi-cloud disk parameter <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## Placement

Location information of the cluster instance

Referenced by API: CreateInstance, InquiryPriceCreateInstance.

| Name | Type | Required | Description |
|------|------|----------|------|
| ProjectId | Integer | Yes | ID of the project to which the instance belongs, which can be obtained in the projectId field returned by calling the DescribeProject API. If this is left empty, default project is used. |
| Zone | String | Yes | ID of the availability zone where the instance is located, which can be obtained in the Zone field returned by calling the DescribeZones API. |

## PreExecuteFileSettings

Pre-execution script configuration

Referenced by API: CreateInstance, ScaleOutInstance.

| Name | Type | Required | Description |
|------|------|----------|------|
| Path | String | Yes | COS path of the script |
| Args | Array of String | Yes | Execution script parameter |
| Bucket | String | Yes | COS bucket name |
| Region | String | Yes | COS region name |
| Domain | String | Yes | COS domain data |

## ResourceSpec

Resource description

Referenced by API: CreateInstance, InquiryPriceCreateInstance.

| Name | Type | Required | Description |
|------|------|----------|------|
| CommonCount | Integer | Yes | Number of common nodes |
| MasterResourceSpec | [NodeSpec](#NodeSpec) | No | Description of master node resources |
| CoreResourceSpec | [NodeSpec](#NodeSpec) | No | Description of core node resources |
| TaskResourceSpec | [NodeSpec](#NodeSpec) | No | Description of task node resources |
| MasterCount | Integer | No | Number of master nodes |
| CoreCount | Integer | No | Number of core nodes |
| TaskCount | Integer | No | Number of task nodes |
| CommonResourceSpec | [NodeSpec](#NodeSpec) | No | Description of common node resources |

## ScaleOutInstanceResult

Instance scale-out result

Referenced by API: ScaleOutInstance.

| Name | Type | Description |
|------|------|-------|
| ClientToken | String | The token passed in during client call |
| InstanceId | String | ID of the instance for scale-out |
| DealNames | Array of String | Order name |

## TerminateResult

Termination request description

Referenced by API: TerminateInstance, TerminateTasks.

| Name | Type | Description |
|------|------|-------|
| InstanceId | String | ID of the terminated cluster |
| ResourceIds | Array of String | Resource ID |

## VPCSettings

VPC parameters

Referenced by API: CreateInstance, InquiryPriceCreateInstance.

| Name | Type | Required | Description |
|------|------|----------|------|
| VpcId | String | Yes | VPC ID |
| SubnetId | String | Yes | Subnet ID |


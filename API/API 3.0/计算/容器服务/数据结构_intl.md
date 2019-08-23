## Cluster

Cluster data structure

Referenced by: DescribeClusters.

| Name | Type | Description |
|------|------|-------|
| ClusterId | String | Cluster ID |
| ClusterName | String | Cluster name |
| ClusterDescription | String | Cluster description |
| ClusterVersion | String | Cluster version (the default value is 1.10.5) |
| ClusterOs | String | Cluster OS. Valid values: Centos7.2x86_64, ubuntu16.04.1 LTSx86_64. Default value: ubuntu16.04.1 LTSx86_64 |
| ClusterType | String | Cluster type. MANAGED_CLUSTER: managed cluster; INDEPENDENT_CLUSTER: independent cluster. |
| ClusterNetworkSettings | [ClusterNetworkSettings](#ClusterNetworkSettings) | Cluster network parameters |
| ClusterNodeNum | Integer | Current number of nodes in the cluster |
| ProjectId | Integer | Project ID of the cluster |

## ClusterAdvancedSettings

Advanced configuration of a cluster

Referenced by: CreateCluster.

| Name | Type | Required | Description |
|------|------|----------|------|
| IPVS | Boolean | No | Whether to enable IPVS |
| AsEnabled | Boolean | No | Whether to enable cluster node scaling |

## ClusterBasicSettings

Describes the basic configuration information of a cluster

Referenced by: CreateCluster.

| Name | Type | Required | Description |
|------|------|----------|------|
| ClusterOs | String | No | Cluster OS. Valid values: Centos7.2x86_64, ubuntu16.04.1 LTSx86_64. Default value: ubuntu16.04.1 LTSx86_64 |
| ClusterVersion | String | No | Cluster version; the default value is 1.10.5 |
| ClusterName | String | No | Cluster name |
| ClusterDescription | String | No | Cluster description |
| VpcId | String | No | VPC ID in the format of vpc-xxx, which is required when an empty managed cluster is created |
| ProjectId | Integer | No | Project ID of new resources in the cluster |

## ClusterCIDRSettings

Cluster container network parameters

Referenced by: CreateCluster.

| Name | Type | Required | Description |
|------|------|----------|------|
| ClusterCIDR | String | Yes | A CIDR that is used to assign containers and service IPs for the cluster, and its value should not conflict with VPC’s CIDR or CIDRs of other clusters within the same VPC |
| IgnoreClusterCIDRConflict | Boolean | No| Whether to ignore the error caused by the value of ClusterCIDR conflicting with VPC’s CIDR or CIDRs of other clusters within the same VPC. Default is No |
| MaxNodePodNum | Integer | No | Maximum number of pods per node in the cluster |
| MaxClusterServiceNum | Integer | No | Maximum number of services in the cluster |

## ClusterNetworkSettings

Cluster network parameters

Referenced by: DescribeClusters.

| Name | Type | Required | Description |
|------|------|----------|------|
| ClusterCIDR | String | Yes | A CIDR that is used to assign containers and service IPs for the cluster, and its value should not conflict with VPC’s CIDR or CIDRs of other clusters within the same VPC |
| IgnoreClusterCIDRConflict | Boolean | No| Whether to not ignore the error caused by the value of ClusterCIDR conflicting with VPC’s CIDR or CIDRs of other clusters within the same VPC. Default is No |
| MaxNodePodNum | Integer | No | Maximum number of pods per node in the cluster (default is 256) |
| MaxClusterServiceNum | Integer | No | Maximum number of services in the cluster (default is 256) |
| Ipvs | Boolean | No | Whether to enable IPVS. Default is No |
| VpcId | String | No| VPC ID of the cluster (which is required when an empty cluster is created; otherwise, it is automatically set to be the same as that of cluster nodes) |

## EnhancedService

The information of enhanced services of this instance, such as Cloud Security, Cloud Monitor and other instance agents.

Referenced by: AddExistedInstances, CreateCluster.

| Name | Type | Required | Description |
|------|------|----------|------|
| SecurityService | [RunSecurityServiceEnabled](#RunSecurityServiceEnabled) | No | Whether to enable Cloud Security. If this parameter is not specified, Cloud Security will be enabled by default. |
| MonitorService | [RunMonitorServiceEnabled](#RunMonitorServiceEnabled) | No | Whether to enable Cloud Monitor. If this parameter is not specified, Cloud Monitor will be enabled by default. |

## ExistedInstancesForNode

Configuration parameters of existing nodes in different roles

Referenced by: CreateCluster.

| Name | Type | Required | Description |
|------|------|----------|------|
| NodeRole | String | Yes | The role the Node plays. Valid values: MASTER_ETCD, WORKER. You only need to specify a value for MASTER_ETCD only when creating an independent cluster (INDEPENDENT_CLUSTER). |
| ExistedInstancesPara | [ExistedInstancesPara](#ExistedInstancesPara) | Reinstallation parameters of existing instances |

## ExistedInstancesPara

Reinstallation parameters of existing instances

Referenced by: CreateCluster.

| Name | Type | Required | Description |
|------|------|----------|------|
| InstanceIds | Array of String | Yes | Cluster ID |
| InstanceAdvancedSettings | [InstanceAdvancedSettings](#InstanceAdvancedSettings) | No | Additional parameters need to be specified for the CVM instance |
| EnhancedService | [EnhancedService](#EnhancedService) | No | Enable or disable enhanced services, including Cloud Security, Cloud Monitoring. If this parameter is not specified, Cloud Monitoring and Cloud Security will be enabled by default  |
| LoginSettings | [LoginSettings](#LoginSettings) | No | Login to Node. Currently, you can only use password or a single KeyId to login to the node. |
| SecurityGroupIds | Array of String | No | Security group of the instance. You may find this parameter in  `sgId` returned by API DescribeSecurityGroups. If this parameter is not specified, the default security group is bound (currently, you can configure only one single `sgId`) |

## Filter

Filter

Referenced by: DescribeClusters.

| Name | Type | Required | Description |
|------|------|----------|------|
| Name | String | Yes | Attribute name. The logical relationship among multiple `Filters` is AND. |
| Values | Array of String | Yes | Attribute values. If a `Filter` has multiple `Values`, the logical relationship among these `Values` is OR. |

## Instance

Cluster instance information

Referenced by: DescribeClusterInstances.

| Name | Type | Description |
|------|------|-------|
| InstanceAdvanceSettings | [InstanceAdvancedSettings](#InstanceAdvancedSettings) | Advanced settings for the instance |
| InstanceId | String | Instance ID |
| InstanceRole | String | Node role. Values include MASTER, WORKER, ETCD, MASTER_ETCD and ALL. The default value is WORKER. |
| FailedReason | String | Reason for instance exception (or initialization) |
| InstanceState | String | Instance status (running, initializing, or failed) |

## InstanceAdvancedSettings

Describes the configuration and information related to the K8s cluster.

Referenced by: AddExistedInstances, CreateCluster, DescribeClusterInstances.

| Name | Type | Required | Description |
|------|------|----------|------|
| MountTarget | String | No | Data disk mounting point. No data disk is mounted by default. Formatted data disks in ext3, ext4, or XFS file system will be mounted directly, while data disks in other file systems and unformatted data disks will be automatically formatted as ext4 and mounted. Please back up your data in advanced. This setting is only applicable to CVM instances with only ONE data disk. |
| DockerGraphPath | String | No | Specified value of dockerd --graph. The default value is /var/lib/docker |
| UserScript | String | No | Base64-encoded user script, which will be executed after the K8s component starts running. It should be ensured that the script's reentrant and retry logics work properly. The script and its generated log files can be checked in the node's `/data/ccs_userscript/` path. If you want to initialize nodes before adding them to the scheduling list, you can use this parameter together with the `unschedulable` parameter. After the final initialization of `userScript` is completed, add the `kubectl uncordon nodename --kubeconfig=/root/.kube/config` command to enable the node for scheduling |
| Unschedulable | Integer | No | Whether the added node is schedulable. 0: schedulable (default value); other values: unschedulable. After the node initialization is completed, you can run `kubectl uncordon nodename` to enable this node for scheduling. |

## LoginSettings

The configuration and information related to instance login.

Referenced by: AddExistedInstances, CreateCluster.

| Name | Type | Required | Description |
|------|------|----------|------|
| Password | String | No | Login password of the instance. The rule of password varies by OS: <br><li>For Linux instances, the password must be a combination of 8-16 characters in at least two of the following types: [a-z, A-Z], [0-9], and [( ) ` ~ ! @ # $ % ^ & * - + = &#124; { } [ ] : ; ' , . ? / ]. <br><li>For Windows instances, the password must be a combination of 12-16 characters in at least three of the following types: [a-z], [A-Z], [0-9] and [( ) ` ~ ! @ # $ % ^ & * - + = { } [ ] : ; ' , . ? /]. <br><br>If this parameter is not specified, a password is randomly generated and sent to you via the internal message. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| KeyIds | Array of String | No | List of key IDs. When an instance is associated with a key pair, it can be accessed using the corresponding private key. KeyId can be obtained through the DescribeKeyPairs API. A key and a password cannot be specified at the same time. Key-pair login is not applicable to Windows instances. You can specify only one key when purchasing an instance. <br/>Note: This field may return null, indicating that no valid values can be obtained. |
| KeepImageLogin | String | No | Whether to keep the original login settings for the image. You cannot specify this parameter when `Password` or `KeyIds.N` is specified. Valid values: <br><li>TRUE: Keep the login settings for the image. This is only applicable when you create an instance using a custom image, shared image, or a image imported from external resources. <br><li>FALSE: Do not keep the login settings for the image <br><br>Default value: FALSE. <br/>Note: This field may return null, indicating that no valid values can be obtained. |

## RunInstancesForNode

Node configuration parameters of different roles

Referenced by: CreateCluster.

| Name | Type | Required | Description |
|------|------|----------|------|
| NodeRole | String | Yes | The role the Node plays. Valid values: MASTER_ETCD, WORKER. You only need to specify a value for MASTER_ETCD only when creating an independent cluster (INDEPENDENT_CLUSTER). |
| RunInstancesPara | Array of String | Yes | A JSON string passed through when create a CVM instance. For more information, see the API for [creating a CVM instance](https://cloud.tencent.com/document/product/213/15730). You only need to pass in a parameter other than the common parameters, where ImageId should be replaced with the ID of the image corresponding to the TKE cluster OS. |

## RunMonitorServiceEnabled

Information on the Cloud Monitor service.

Referenced by: AddExistedInstances, CreateCluster.

| Name | Type | Required | Description |
|------|------|----------|------|
| Enabled | Boolean | No | Whether to enable [Cloud Monitor](/document/product/248). Valid values: <br><li>TRUE: Yes <br><li>FALSE: No <br><br>Default value: TRUE. |

## RunSecurityServiceEnabled

Information on the Cloud Security service

Referenced by: AddExistedInstances, CreateCluster.

| Name | Type | Required | Description |
|------|------|----------|------|
| Enabled | Boolean | No | Whether to enable [Cloud Security](/document/product/296). Valid values: <br><li>TRUE: Yes <br><li>FALSE: No <br><br>Default value: TRUE. |


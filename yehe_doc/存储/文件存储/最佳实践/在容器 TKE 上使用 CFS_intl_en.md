## Overview

CFS is suitable for two use cases in a container environment:

#### Use case 1. Persistent storage of Pod/container data (dynamic mounting of CFS recommended)

CFS provides a space for persistent storage where the data is still stored when a Pod or container is terminated. In this way, the original space can be quickly mounted through PVCs to implement data reads/writes quickly when another Pod or container is started.
Compared with other schemes, a single-FS instance allows you to store the data from multiple Pods or containers and assign different subdirectories in the CFS instance to different Pods. Standard and High-Performance CFS instances are pay-as-you-go with no requirement for the minimum purchase capacity. This helps reduce the costs of persistent data storage for large-scale containers.

#### Use case 2. Multi-Pod/container data sharing (static mounting of CFS recommended)

CFS provides shared access to a directory space from multiple Pods or containers over NFS or private protocols for efficient data sharing. Compared with other schemes, this provides higher bandwidth and IOPS capabilities.

This document describes how to deploy a container workload in the Tencent Cloud console. For more information on how to write a YAML file, refer to the YAML file automatically generated after a StorageClass is created in the console.

>! Make sure that the CSI component in the TKE cluster is on v1.0.4 or later; otherwise, update it in the TKE console. The updating operation does not affect the normal use of the container.
>

## Directions

### Dynamically mounting CFS

>? This mounting option is recommended for persistent storage of Pod/container data.
>

1. Create a StorageClass as instructed in [Managing CFS Templates by Using a StorageClass](https://intl.cloud.tencent.com/document/product/457/36154).

Key configuration items are as described below:
<table>
	<tr><th>Configuration Item</th><th>Description</th></tr>
	<tr><td>Instance creation mode</td><td>Select <b>Shared instance</b>.</td></tr>
	<tr><td>Availability zone</td><td>We recommend you select the same AZ as that of the container host.</td></tr>
	<tr><td>Storage type</td><td>Select <b>Standard</b>. or <b>High-performance</b>. as needed.</td></tr>
	<tr><td>Protocol version</td><td>Unless in scenarios involving concurrent modifications, we recommend you use the NFS v3 protocol for a higher performance.</td></tr>
	<tr><td>Reclaim policy</td><td>Select <b>Delete</b>. or <b>Retain</b>. as needed. To avoid mistaken data deletion, we recommend you select <b>Retain</b>..</td></tr>
</table>


2. Create a PVC as instructed in [Managing CFS by Using PVs and PVCs](https://intl.cloud.tencent.com/document/product/457/36155).

Key configuration items are as described below:
<table>
	<tr><th>Configuration Item</th><th>Description</th></tr>
	<tr><td>Namespace</td><td>Select a namespace as needed.</td></tr>
	<tr><td>StorageClass</td><td>Select the just created StorgeClass.</td></tr>
	<tr><td>PersistentVolume</td><td>You don't need to specify a PV for dynamic creation.</br><b>Note</b>: For a StorageClass based on a shared CFS instance, if you don't specify a PV when creating a PVC, the CSI plugin will automatically create a pay-as-you-go CFS instance when creating a PVC. This instance will be deleted when the PVC is deleted. Therefore, process PVCs created in this way with caution.</td></tr>
</table>

3. Create a Deployment as instructed in [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662).

Key configuration items are as described below:
<table>
	<tr><th>Configuration Item</th><th>Description</th></tr>
	<tr><td>Volume</td><td>Name the volume as needed and select the just created PVC.</td></tr>
	<tr><td>Mount point</td><td>Select the volume and specify the path for mounting to the container. When you dynamically create a shared CFS instance, you need to specify an environment variable, and the CSI plugin will create a directory in the CFS instance corresponding to the selected PVC based on the value of the configured environment variable for the container to mount.</td></tr>
</table>
After completing the configuration, click <b>Create Workload</b>, and the system will create a container based on this configuration and mount CFS.


### Statically mounting CFS

>? This mounting option is recommended for multi-Pod/container data sharing.
>

1. Create a StorageClass as instructed in [Managing CFS Templates by Using a StorageClass](https://intl.cloud.tencent.com/document/product/457/36154).

Key configuration items are as described below:
<table>
	<tr><th>Configuration Item</th><th>Description</th></tr>
	<tr><td>Instance creation mode</td><td>Select <b>.Shared instance</b>..</td></tr>
	<tr><td>Availability zone</td><td>We recommend you select the same AZ as that of the container host.</td></tr>
	<tr><td>Storage type</td><td>Select <b>.Standard</b>. or <b>.High-performance</b>.as needed.</td></tr>
	<tr><td>Protocol version</td><td>Unless in scenarios involving concurrent modifications, we recommend you use the NFS v3 protocol for a higher performance.</td></tr>
	<tr><td>Reclaim policy</td><td>Select <b>.Delete</b>. or <b>.Retain</b>. as needed. To avoid mistaken data deletion, we recommend you select <b>.Retain</b>..</td></tr>
</table>

2. Create a PV as instructed in [Managing CFS by Using PVs and PVCs](https://intl.cloud.tencent.com/document/product/457/36155).

Key configuration items are as described below:
<table>
	<tr><th>Configuration Item</th><th>Description</th></tr>
	<tr><td>Creation method</td><td>Select <b>.Manual</b>.; that is, specify a CFS instance for PV configuration.</td></tr>
	<tr><td>StorgeClass</td><td>Select the just created StorgeClass.</td></tr>
	<tr><td>Select CFS</td><td>Select a specified CFS instance.</br><b>Note</b>: During dynamic creation, make sure that you already have a CFS instance in the same VPC as the container.</td></tr>
	<tr><td>CFS sub-directory</td><td>CFS allows you to mount sub-directories. You can select different subdirectories and bind them to one or multiple PVs as needed to implement different degrees of data sharing.</td></tr>
</table>

3. Create a PVC as instructed in [Managing CFS by Using PVs and PVCs](https://intl.cloud.tencent.com/document/product/457/36155).

Key configuration items are as described below:
<table>
	<tr><th>Configuration Item</th><th>Description</th></tr>
	<tr><td>Namespace</td><td>Select a namespace as needed.</td></tr>
	<tr><td>StorageClass</td><td>Select the just created StorgeClass.</td></tr>
	<tr><td>PersistentVolume</td><td>Select <b>.Specify</b>. and select the just created PV.</td></tr>
</table>

4. Create a Deployment as instructed in [Deployment Management](https://intl.cloud.tencent.com/document/product/457/30662).

Key configuration items are as described below:
<table>
	<tr><th>Configuration Item</th><th>Description</th></tr>
	<tr><td>Volume</td><td>Name the volume as needed and select the just created PVC.</td></tr>
	<tr><td>Mount point</td><td>Select the volume and specify the path for mounting to the container. To specify a sub-path of the file system for mounting, make sure that the directory exists, which does not need to start with `/`. </br>If the directory does not exist, and you want the container to automatically create one, you can specify an environment variable, and the CSI plugin will automatically create the directory in the root path of the file system with the name of the variable value and provide it to the container for mounting.</td></tr>
</table>
After completing the configuration, click <b>Create Workload</b>, and the system will create a container based on this configuration and mount CFS.


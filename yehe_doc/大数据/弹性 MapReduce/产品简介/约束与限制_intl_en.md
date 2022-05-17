Before using EMR, carefully read and understand the following use limits:
- To ensure the cluster network security, new clusters will be placed in the same VPC. Do not change the VPC of an existing cluster or node; otherwise, the cluster network may fail.
- When you create a cluster, EMR can help you create a new security group, or you can also manually select an existing EMR security group. Make sure that the selected security group has the necessary inbound/outbound rules for EMR. Do not delete or change the security group in use after creating the cluster; otherwise, cluster communication may fail, thus affecting the service.
- Plan the storage space of nodes in advance based on your business needs, and promptly add storage nodes, as an insufficient storage space may cause data and node risks. Currently, core, task, and router nodes in the EMR cluster support mounting multiple cloud disks, and a node can have up to 15 cloud disks. Clusters in BM 2.0 and local disk models (IO and D series) don't support mounting multiple cloud disks.
- When using EMR, do not perform operations in the CVM console, such as shutdown, restart, VPC switch, security group rule adjustment, so as to avoid cluster exceptions. OS reinstallation, instance termination, configuration adjustment, renewal, and billing mode change are also not recommended. You can perform necessary cluster maintenance operations in the EMR console.
- Public IPs can increase the possibility of master nodes being attacked, so you need to manage and monitor the risks. EIPs (including the IPs on the secondary ENI) will be retained after the cluster is terminated, and the idle IPs will continue to incur fees. If you don't need to retain them, release them on the corresponding resource management page.
- When you create a cluster, EMR provides component initialization parameters for general scenarios. Before you use components such as HDFS and HBase, we recommend you check whether the component parameters meet the needs of your business scenarios. To get the component initialization guide, contact us.
- Keep the host login password of your EMR cluster secure. If you configure passwordless login for cross-node access, Tencent Cloud security services may detect vulnerability risks and prompt you.
- Even if an exception occurs in your cluster, the cluster will continue to be billed. In this case, we recommend you promptly contact us for assistance. If we need to log in to your cluster for troubleshooting, we will gain your consent and ask for your account password.

When you use or maintain your EMR cluster, some unexpected operations may render it unavailable or unstable, and you will receive a risk warning before performing such operations in the console. This document lists some of the prohibited and risky operations:
## Prohibited Operations

<table>
<thread>
<tr>
<th >Operation</th>
<th >Risk</th>
</tr>
</thread>
<tr>
<td >Change the private IP of an EMR node in CVM</td>
<td >Node communication exception or cluster unavailability</td>
</tr><tr>
<td >Modify the security group of a CVM node while the cluster is running</td>
<td >Node communication exception or component service unavailability</td>
</tr><tr>
<td >Delete an existing process, application, or file from a node</td>
<td >Cluster/Component service unavailability</td>
</tr><tr>
<td >Delete or modify the `hosts` file in the `/etc` directory</td>
<td >Service exception, as the cluster cannot be associated with the service on the node</td>
</tr><tr>
<td >Delete or modify the HDFS metadata file `edit log`</td>
<td >HDFS cluster unavailability</td>
</tr><tr>
<td >Manually modify the data in the Hive metadatabase</td>
<td >Service exception caused by a Hive data parsing error</td>
</tr><tr>
<td >Delete a ZooKeeper data directory</td>
<td >Failure of dependent components</td>
</tr>
</table>
     
## Risky Operations
<table>
<thread>
<tr>
<th >Operation</th>
<th >Risk</th>
<th >Suggestion</th>
</tr>
</thread>
<tr>
<td >Shut down or restart an EMR cluster node in CVM</td>
<td >Service unavailability</td>
<td >Check whether the operation is necessary and read the CVM operation limits</td>
</tr><tr>
<td >Mount a disk to an EMR node in the CVM console</td>
<td >Disk unavailability caused by EMR's failure to recognize and initialize the disk</td>
<td >Do this through core node scaling or under technical guidance</td>
</tr><tr>
<td >Unmount a disk from an EMR node in the CVM console</td>
<td >Data loss or cluster unavailability</td>
<td >Do this through core node scaling or under technical guidance</td>
</tr><tr>
<td >Modify the component configuration file parameters in CVM</td>
<td >Modified parameter overwrite after service restart</td>
<td >Modify the parameter configuration in the EMR console and seek technical guidance in special circumstances</td>
</tr><tr>
<td >Delete or modify the `resolv.conf` file in the `/etc` directory</td>
<td >Service exception, as the cluster cannot be associated with the service on the node</td>
<td >Check whether the operation is necessary and perform it under technical guidance</td>
</tr><tr>
<td >Modify the MetaDB password</td>
<td >EMR depends on the password configured in MetaDB, and after the password is changed, services such as Hive and Ranger will become unavailable</td>
<td >Modify the configuration in the EMR console under technical guidance</td>
</tr><tr>
<td >Modify the MetaDB floating IP</td>
<td >Hive and Ranger service unavailability, as EMR depends on the IP configured in MetaDB</td>
<td >Modify the configuration in the EMR console under technical guidance</td>
</tr><tr>
<td >Modify the MetaDB security group</td>
<td >Interruption of the communication between MetaDB and the cluster, or Hive and Ranger service unavailability</td>
<td >Perform the operation under technical guidance</td>
</tr>
</table>

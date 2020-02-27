## Scenarios
In many TKE scenarios, such as Kubernetes version upgrade and kernel version upgrade, you must remove the node and then add it back. This document describes the process of removing and re-adding a node in detail. This operation can be divided into the following steps:
1. Drain the Pods running on the node.
2. Remove the node from the cluster, and then re-add it to the cluster. This node will reinstall the system.
3. Remove the cordon.

## Considerations
- If multiple nodes on a single cluster all need to be removed and added back, it is recommended that you do so node by node. That is, complete the removal and addition of a single node and verify that the service is normal, and then remove the next node and add it back, completing multiple nodes successively.
- If multiple clusters in a single account need to have their nodes removed and added back, it is recommended that the operation be executed in batches. After the operation has been completed on each cluster, verify whether the cluster status is normal.


## Directions
### Step 1: drain Pods
Before performing the removal and re-addition of a node in a cluster, you must first drain the Pods on the node to be removed to have them operate on a different node. The draining process involves deleting the Pods on the node one by one, and then reconstruct them on another node. For more information about this operation, see [Principles of draining](#drain).


#### Checking before draining
The draining process involves reconstructing Pods, which may affect services in the cluster. Therefore, it is recommended that you perform the following checks before performing draining:
1. Check whether the remaining nodes in the cluster have sufficient resources to run the Pods on the node to be drained.
You can check the resource allocation of the nodes in TKE Console. In the **[Cluster List](https://console.cloud.tencent.com/tke2/cluster)** page, select the cluster ID > **Node Management** >  and the node, and check the **Assigned/Total Resources** on the **Node List** page. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/5ac6f7f2000b2389c4546c3e08644978.png)
	If the remaining resources of the nodes are insufficient, it is recommended that you add new nodes to the cluster to prevent the drained Pod from being unable to run and, as a result, affecting the service.
2. Check whether active drainage protection, PodDisruptionBudget (PDB), is configured in the cluster.
Active drainage protection interrupts the execution of drainage operations. It is recommended that you first delete the active drainage protection PDB.
3. Check whether all the Pods of a single service are on the node to be drained.
If all the Pods of a single service are located on the same node, draining the Pods will make the entire service unavailable. Please determine whether the service needs all Pods to be located on the same node.
	- If not, it is recommended that you add anti-affinity scheduling.
	- If so, it is recommended that you perform the operation during periods of low or no traffic.
4. Check if the service uses a local disk (hostpath).
If the service uses the `hostpath volume` method, when the Pod is scheduled to another node, the data will be lost which may affect the business. If the data is important, back it up before draining.

> Currently, kubelet’s image pull policy is serial. If a large number of Pods is scheduled to the same node in a short period of time, the Pod launch time may be longer.


#### Specific directions

Currently, there are two ways to complete drainage for TKE clusters:
- Drain in TKE Console.
- Use the `kubectl drain` command.

**Drain in TKE Console**
1. On the Cluster List page, select the cluster ID of the node to be drained, and enter the Cluster Workload Management page.
2. On the left sidebar, select **Node Management** > **Node** to go to the **Node List** page.
3. On the right of the row where the node is located, select **More** > **Drain** to drain the Pods running on the node. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/77764afa7d3ba6192a1d13d4d8169c65.png)

**Using the kubectl drain command to drain**
1. To log in to the node, refer to [Logging In to a Linux Instance in Standard Login Mode (Recommended)](https://intl.cloud.tencent.com/document/product/213/5436).
2. Execute the following command to drain the Pods on this node.
```
kubectl drain node <node-name>
```

### Step 2: remove the node
>When the Pods running on a node are drained, this node is cordoned.
>
1. In the **Node List** page, click **Remove** on the right of the row where the node is located.
2. In the pop-up window, uncheck **Terminate pay-as-you-go nodes** and click **OK** to remove the node from the cluster. This is shown in the following figure:
>
>- Note the node ID to be used for re-adding the node to the cluster.
>- Be careful not to check **Terminate pay-as-you-go nodes**, as they cannot be restored after being terminated.
>
![](https://main.qcloudimg.com/raw/8231695c9f69b6690a2164dfe32d08a4.png)


### Step 3: add the node back to the cluster
1. In the **Node List** page, click **Add Existing Node** on the top of the page.
2. On the **Select Nodes** page, enter the recorded node ID and click <img src="https://main.qcloudimg.com/raw/706ad377ac9c152afe7d28aa9685f8e6.png" style="margin:-3px 0px">.
3. In the search results list, check the desired node and click **Next** to go to the CVM Configuration page. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/23bb5511c4b49ce16a50d45c983416ba.png)
4. In the **CVM Configuration** page, **Mount Data disk** and **Container Directory** are not checked by default. If you need to store the container and image on the data disk, please check **Mount Data disk**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/e25bdb6fd89a23744528019eedec60d1.png)
>When *Mount data disk** is selected, the system disk with an formatted ext3, ext4 or xfs file system will be mounted directly. Other file systems or unformatted data disks will be automatically formatted as ext4, and mounted. If you need to keep the data disk and mount it, you can refer to [Data Disk Mounting](#data).
>
5. Set the login password and security group according to your actual circumstances, click **Complete**, and wait for the node to be added successfully.


### Step 4: remove the cordon
>After the node is added successfully, it is still cordoned.
>
1. In the **Node List** page, select **More** > **Uncordon** on the right of the row where the node is located.
2. In the pop-up window, click **OK** to remove the cordon.

## Notes

### Principles of draining<span id="drain"></span>

To streamline node maintenance operations, Kubernetes introduced the `drain` command. The use principles are as follows:

For versions after Kubernetes 1.4, the `drain` operation is to first cordon the node and then delete all the Pods on the node. If this Pod is managed by a controller such as Deployment, the controller will re-construct the Pod when it detects that the number of Pod replicas has decreased, and will schedule them to other nodes that meet the conditions. If this Pod is a bare Pod that is not managed by a controller, it will not be re-constructed after it is drained.

This process involves first deleting, and then re-creation, and is not a rolling update. Therefore, in the update process, some requests for drained services may fail. If all the related Pods of the drained service are on the drained node, the service may become completely unavailable.

To avoid this situation, Kubernetes versions 1.4 and later introduced PodDisruptionBudget (PDB). You only need to select a business (a group of Pods) in the PDB policy file, to declare the minimum number of replicas that this business can tolerate. Now when you execute the `drain` operation, the Pod is no longer deleted directly, but instead whether it meets the PDB policy is checked through `evict api`. The Pods will only be deleted if the PDB policy is satisfied, protecting business availability. Note that the impact of the `drain` operation on businesses can only be controlled if PDB is correctly configured.

### Data disk mounting<span id="data"></span>

>Through this step, you can mount the data disk without formatting it. 
>
1. In the **CVM Configuration** page, do not check **Mount Data Disk**.
2. Open **Advanced Configurations**. In the **Custom Data** enter the following node initialization script and place a check next to **Enable Cordon**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/2998c7dcebca9bcff89fcf0d38586fc9.png)
```
systemctl stop kubelet  
docker stop $(docker ps -a | awk '{ print $1}' | tail -n +2)
systemctl stop dockerd  
echo '/dev/vdb   /data    ext4   noatime,acl,user_xattr 1 1' >> /etc/fstab
mount -a
sed -i 's#"graph": "/var/lib/docker",#"data-root": "/data/docker",#g' /etc/docker/daemon.json
systemctl start dockerd  
systemctl start kubelet 
```
3. Set the login password and security group according to your actual circumstances, click **Complete**, and wait for the node to be added successfully.

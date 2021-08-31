This document describes the FAQs of EKS cluster and the corresponding solutions.

### Why is the Pod specification inconsistent with the set Request/Limit?

When allocating the resources for Pod, EKS will calculate the Request and Limit set by the workload, and automatically determine the amount of resources required for running the Pod, instead of allocating resources according to the set Request and Limit values. For more information, see [CPU specifications calculation methods for pods](https://intl.cloud.tencent.com/document/product/457/36161) and [GPU specification calculation methods for pods](https://intl.cloud.tencent.com/document/product/457/36161).




### How to create or modify the container network of the EKS cluster?

When creating a cluster, you need to select a VPC as the cluster network and specify a subnet as the container network. For more information, see [Notes on the Container Network](https://intl.cloud.tencent.com/document/product/457/ 34048). The Pod of EKS directly occupies an IP address of the container network subnet. When using the cluster, you can create or modify the container network through creating or removing the virtual node. The detailed instructions are shown below.

[](id:create)

#### Step 1: Create a virtual node to create a container network.

1. Log in to the TKE console, click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar, and click the ID of the cluster that you want to modify the container network.
2. In the cluster details page, click **Virtual Node** in the left sidebar, and then click **Create Virtual Node**.
3. In **Create Virtual Node** page, select the container network with sufficient IPs and click **OK**.
   ![](https://main.qcloudimg.com/raw/e23c76930b29b81f4ba0b48f92197bf4.png)

#### Step 2: Remove the virtual node to delete the container network.

<dx-alert infotype="notice" title="">
At least one virtual node is required for the EKS cluster. If there is only one virtual node, it cannot be removed.
</dx-alert>

Before removing a virtual node, you need to drain all Pods on this virtual node to other virtual nodes (not including Pods managed by DaemonSet). After the draining is completed, you can remove the virtual node, otherwise the node will fail to remove. The detailed instructions are shown below.

1. Log in to the TKE console, click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar, and click the ID of the cluster that you want to drain the virtual node.
2. In the cluster details page, click **Virtual Node** in the left sidebar to go to the **Virtual Node** page. Select the virtual node to drain, and click **More** > **Drain** in the **Operation** column.
   ![](https://main.qcloudimg.com/raw/60e0e68228c1721de29f03e74236a062.png)
3. In the **Drain Node** window, click **OK**.
   <dx-alert infotype="notice" title="">
   Once drained, the Pod will be rebuilt.
   </dx-alert>
    After being drained, the status of the virtual node will be changed to "Cordoned", and no more Pods will be scheduled to this node.
4. In the **Virtual Node** page, select the virtual node to remove and click **Remove** in the **Operation** column.
5. In the **Delete Node** window, click **OK**.




### What should I do if the Pod fails to schedule because of insufficient subnet IPs?

When the Pod fails to schedule because of the insufficient subnet IPs, you can find two events in the node logs, as shown below:

- Event 1:
  ![](https://main.qcloudimg.com/raw/da4980efe001e7a4a6cbd9c14b0451ec.png)
- Event 2:
  ![](https://main.qcloudimg.com/raw/eb021a08ade02738992c896b6ed1d5d5.png)

You can query the YAML of the virtual node via the [TKE console](https://console.cloud.tencent.com/tke2/ecluster?rid=1) or running the following command in the command line tool.

```sh
kubectl get nodes -oyaml
```

The following information will appear:

```yaml
spec:
   taints:
   - effect: NoSchedule
     key: node.kubernetes.io/network-unavailable
     timeAdded: "2021-04-20T07:00:16Z"
```

```yaml
- lastHeartbeatTime: "2021-04-20T07:55:28Z"
      lastTransitionTime: "2021-04-20T07:00:16Z"
      message: eklet node has insufficient IP available of subnet subnet-bok73g4c
      reason: EKLetHasInsufficientSubnetIP
      status: "True"
      type: NetworkUnavailable
```

It shows that the Pod fails to schedule because the subnet IPs of the container network is insufficient. In this case, you need to create virtual nodes to add subnets to add available IP ranges for the cluster Pod. For how to create a virtual node, see [Create a Virtual Node](#create).



### What are the instructions for using the EKS security group?

When creating the EKS cluster Pod, if you do not specify a security group, the default security group will be used. You can also specify security group for the Pod through `Annotation eks.tke.cloud.tencent.com/security-group-id: security group ID`. Please ensure that the security group ID already exists in the region where the workload resides. For more information on this annotation, see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).

### How do I set the container termination message?



Kubernetes can set the message source of the container exit through `terminationMessagePath`, that is, when the container exits, Kubernetes will retrieve termination messages from the termination message file specified in the `terminationMessagePath` field of a container, and use this contents from the specified file to populate the container's termination message. The default value of the message is `/dev/termination-log`.

Moreover, you can set the `terminationMessagePolicy` field of a container for further termination message customization. This field defaults to “File”, which means the termination messages are retrieved only from the termination message file. You can set the `terminationMessagePolicy` to `FallbackToLogsOnError` as needed, and Kubernetes will use the last chunk of container log output if the termination message file is empty and the container exited with an error.

The code sample is shown as follows:


```yaml
apiVersion: apps/v1beta2
kind: Deployment
metadata:
     name: nginx
spec:
      containers:
      - image: nginx
        imagePullPolicy: Always
        name: nginx
        resources:
          limits:
            cpu: 500m
            memory: 1Gi
          requests:
            cpu: 250m
            memory: 256Mi
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: FallbackToLogsOnError
```

With the above configuration, when the container exits with an error and the termination message file is empty, Get Pod will find that the output of stderr is displayed in containerStatuses, as shown in the following figure:
![](https://main.qcloudimg.com/raw/cc88807047bf99690de2c3e5ea4adc6c.png)


### What are the instructions for the Host parameter?

When using EKS clusters, you need to pay attention to the following:

There are no nodes in EKS cluster. Although EKS allows Pod to contain host-related parameters, such as Hostpath, Hostnetwork (set to true), DnsPolicy (set to ClusterFirstWithHostNet), EKS clusters may not meet the expected effect. For example, you want to share data through Hostpath, but two Pods scheduled to the same virtual node may have Hostpaths of different hosts, and when the Pod is rebuilt, the Hostpath files will be deleted at the same time. Therefore, the data cannot be shared through Hostpath.

Therefore, we recommend that the tasks you run on the EKS cluster do not strongly depend on Host-related parameters.


### How do I mount CFS/NFS?

In EKS clusters, you can use Tencent Cloud's [Cloud File Storage (CFS)](https://intl.cloud.tencent.com/document/product/582/9127) or mount an external NFS file storage as a Volume to Pod, so as to achieve persistent data storage. A YAML example of Pod mounting CFS/NFS is shown below

<dx-codeblock>
:::  yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
  - image: k8s.gcr.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /cache
      name: cache-volume
    volumes:
  - name: nfs
        nfs:
          path: /dir
          server: 127.0.0.1
    :::
    </dx-codeblock>


- spec.volumes: Set the name, type, and parameters of the volume.
- spec.volumes.nfs: Set the NFS/CFS disk.
- spec.containers.volumeMounts: Set the mount point of the volume in the Pod.

For the detailed operation of Pod mounting Volume, see [Instructions for Other Storage Volumes](https://intl.cloud.tencent.com/document/product/457/30678).

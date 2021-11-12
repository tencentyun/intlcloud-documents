This document summarizes the FAQs of EKS cluster, the causes for these FAQs and the corresponding solutions.

<dx-accordion>

::: Why are the specifications of the Pod inconsistent with the filled-in Request/Limit? [](id:FAQ1)

[](id:1) When allocating the resources for Pod, EKS will calculate the Request and Limit set by the workload, and automatically determine the amount of resources required for running the Pod, instead of allocating resources according to the set Request and Limit values. For more information, see [CPU specifications calculation methods for pods](https://intl.cloud.tencent.com/document/product/457/36161) and [GPU specification calculation methods for pods](https://intl.cloud.tencent.com/document/product/457/36161).

:::


::: How to create or modify the container network of EKS cluster? [](id:FAQ2)

When creating a cluster, you need to select a VPC as the cluster network and specify a subnet as the container network. For more information, see [Notes on the Container Network](https://intl.cloud.tencent.com/document/product/457/ 34048). The Pod of EKS directly occupies an IP address of the container network subnet. When using the cluster, you can create or modify the container network through creating or removing the virtual node. The detailed instructions are shown below.

#### Step 1: Create a virtual node to add a new container network. [] (id:create)

1. Log in to the TKE console, click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar, and click the ID of the cluster that you want to modify the container network.
2. On the cluster details page, click **Virtual Node** in the left sidebar, and then click **Create Virtual Node**.
3. On **Create Virtual Node** page, select the container network with sufficient IPs and click **Confirm**.
   ![](https://main.qcloudimg.com/raw/e23c76930b29b81f4ba0b48f92197bf4.png)


#### Step 2: Remove the virtual node to delete the container network.

<dx-alert infotype="notice" title="">
At least one virtual node is required for the elastic cluster. If there is only one virtual node, it cannot be removed.
</dx-alert>

Before removing a virtual node, you need to drain all Pods on this virtual node to other virtual nodes (not including Pods managed by DaemonSet). After the draining is completed, you can remove the virtual node, otherwise the node will fail to remove. The detailed instructions are shown below.

1. Log in to the TKE console, click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar, and click the ID of the cluster that you want to remove the virtual node.
2. On the cluster details page, select **Virtual Node** in the left sidebar, and select **More** > **Drain** on the right of the node name. See the figure below:
   ![](https://main.qcloudimg.com/raw/60e0e68228c1721de29f03e74236a062.png)
3. In the **Drain Node** window, click **OK**.
   <dx-alert infotype="notice" title="">
   Once drained, the Pod will be rebuilt.
   </dx-alert>
    After being drained, the status of the virtual node will be changed to "Cordoned", and no more Pods will be scheduled to this node.
4. On the **Virtual Node** page, select the virtual node to remove and click **Remove** on the right.
5. In the **Delete Node** window, click **OK**.

:::


::: How to deal with if the Pod fails to schedule because of the insufficient subnet IPs? [](id:FAQ3)

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

:::

::: What about the guidelines and instructions for use of EKS security group? [](id:FAQ4)

When creating the elastic cluster Pod, if you do not specify a security group, the default security group will be used. You can also specify security group for the Pod through `Annotation eks.tke.cloud.tencent.com/security-group-id: security group ID`. Please ensure that the security group ID already exists in the region where the workload resides. For more information on this annotation, see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).
:::
::: How to set container’s termination message? [](id:FAQ5)


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

With the above configuration, when the container exits with an error and the termination message file is empty, Get Pod will find that the output of stderr is displayed in containerStatuses.

:::
::: How to use Host parameters? [](id:FAQ6)

Please note the following when using elastic clusters:

Elastic cluster does not have node, but it is compatible with Host related parameters, such as Hostpath, Hostnetwork: true, DnsPolicy: ClusterFirstWithHostNet.

Please note that, because there is no node, the capacity to provide these parameters can not be fully aligned with that of the standard K8s.

For example, it is expected to use Hostpath to share data, but the two Pods scheduled to the same virtual node see the Hostpath of different sub-machines. If the Pod is rebuilt, files of Hostpath are deleted at the same time.

:::
::: How to mount CFS/NFS? [](id:FAQ7)

In elastic clusters, you can use Tencent Cloud's [Cloud File Storage (CFS)](https://intl.cloud.tencent.com/document/product/582/9127) or mount an external NFS file storage as a Volume to Pod, so as to achieve persistent data storage. A YAML example of Pod mounting CFS/NFS is shown below:

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


:::
::: How to speed up container start-up by image reuse?
EKS supports caching container images to speed up the start-up the next time you start up a container with the same image.

**Conditions for Reuse:**

1. For the Pod of the same workload, if a Pod is created and terminated at the same availability zone (zone) within the cache time, the newly created Pod will not pull the same image by default.
2. If the Pods of different workloads (including Deployment, Statefulset, and Job) want to reuse a image, the following annotation can be used:
```
eks.tke.cloud.tencent.com/cbs-reuse-key
```
For the Pods with the same annotation value under the same user account, the start-up image will be reused within cache time as much as possible. It is recommended to enter the image name of the annotation value: **eks.tke.cloud.tencent.com/cbs-reuse-key: "image-name"**.

**Cache time:** 48 hours.


:::
::: Instructions for exceptional image reuse [](id:FAQ9)
When image reuse function is enabled, if a Pod is created, `$kubectl describe pod` may see the following errors:

- `no space left on device: unknown`
- `Warning FreeDiskSpaceFailed 26m eklet, eklet-subnet-xxx failed to garbage collect required amount of images. Wanted to free 4220828057 bytes, but freed 3889267064 bytes`

**Methods for Resume:**

No action is required. Wait for a few minutes and the Pod will run automatically.
<br>
**Cause:**

- `no space left on device: unknown`
When the Pod reuses the system disk by default, the original image in the system disk occupies all of the disk space, and the disk currently does not have enough space to download the new image, so the error "no space left on device: unknown" is reported. EKS supports a regular image repossess mechanism. When the disk space is full, it will automatically delete the existing redundant images in the system disk to make free space for the current disk. (It takes several minutes)

- `Warning FreeDiskSpaceFailed 26m eklet, eklet-subnet-xxx failed to garbage collect required amount of images. Wanted to free 4220828057 bytes, but freed 3889267064 bytes`
This log shows that the current Pod needs 4220828057 space to download the image, but currently only 38892670644 space is available. The reason for this event is that there are multiple images on the disk. Currently, only some images have been cleaned up. EKS's regular image repossess mechanism will continue to clean up the images until a new image can be successfully pulled.



:::
::: When you mount an external NFS, the event Operation not permitted is reported [](id:FAQ10)

If you use an external NFS to achieve persistent storage, the event Operation not permitted is reported when connecting. You need to modify the /etc/exports file of the external NFS and add the /&lt;path&gt;&lt;ip-range&gt;(rw,insecure) parameter. See example as below:
```
/data/  10.0.0.0/16(rw,insecure)
```

:::
</dx-accordion>

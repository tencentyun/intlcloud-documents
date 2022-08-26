This document summarizes the FAQs, causes, and solutions regarding EKS clusters.

 

### Why is the Pod specification inconsistent with the set `Request` and `Limit` values?[](id:FAQ1)

[](id:1) When allocating the resources for Pod, EKS will calculate the Request and Limit set by the workload, and automatically determine the amount of resources required for running the Pod, instead of allocating resources according to the set Request and Limit values. For more information, see [CPU specifications calculation methods for pods](https://intl.cloud.tencent.com/document/product/457/36161) and [GPU specification calculation methods for pods](https://intl.cloud.tencent.com/document/product/457/36161).

---


### How do I create or modify the container network of an EKS cluster?[](id:FAQ2)

When creating a cluster, you need to select a VPC as the cluster network and specify a subnet as the container network. For more information, see [Notes on the Container Network](https://intl.cloud.tencent.com/document/product/457/34048). The Pod of EKS directly occupies an IP address of the container network subnet. When using the cluster, you can create or modify the container network through creating or removing the super node. The detailed instructions are shown below.

#### Step 1: Create a super node to add a container network[](id:create)

1. Log in to the TKE console, click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar, and click the ID of the cluster for which you need to modify the container network.
2. On the cluster details page, click **super node** in the left sidebar to enter the **super node** page, and click **Create super node**.
3. On the **Create super node** page, select the container network with sufficient IP addresses and click **OK**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/28da152bf95cd0c8eb1898c50955547c.png)


#### Step 2: Remove the super node to delete the container network

<dx-alert infotype="notice" title=" ">
Make sure that at least one super node remains in the elastic cluster after the removal. If there is only one super node, you cannot remove it.
</dx-alert>

Before removing a super node, you need to drain all Pods on it (excluding those managed by DaemonSet) to other super nodes. After the draining is completed, you can remove the super node; otherwise, the removal will fail. The detailed directions are as shown below.

1. Log in to the TKE console, click **[Elastic Cluster](https://console.cloud.tencent.com/tke2/ecluster)** in the left sidebar, and click the ID of the cluster from which you need to remove the super node.
2. On the cluster details page, select **Super node** in the left sidebar, and click **More** > **Drain** on the right of the node name.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e6f6450c760f8d76f5b45146b74238d8.png)
3. In the **Drain node** window, click **OK**.
   <dx-alert infotype="notice" title=" ">
   Note that Pods will be rebuilt once the node is drained.
   </dx-alert>
    After the node is drained, it will enter the "Blocked" status, and no more Pods can be scheduled to it.
4. On the **Super node** page, click **Remove** on the right of the node name.
5. In the **Delete node** pop-up window, click **OK**.

---


### What should I do if a Pod fails to be scheduled due to insufficient subnet IP addresses?[](id:FAQ3)

When a Pod fails to be scheduled due to insufficient subnet IP addresses, you can find two events in the node logs.

- Event 1:
  ![](https://qcloudimg.tencent-cloud.cn/raw/632e4e3182548067ffe48939f475a03b.png)
- Event 2:
  ![](https://main.qcloudimg.com/raw/eb021a08ade02738992c896b6ed1d5d5.png)



You can query the YAML of the super node in the [TKE console](https://console.cloud.tencent.com/tke2/ecluster?rid=1) or by running the following command in the command line tool.

```sh
kubectl get nodes -oyaml
```

The returned result is as follows:

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

It shows that the Pod fails to be scheduled due to insufficient subnet IP addresses of the container network. In this case, you need to create super nodes to add subnets and available IP ranges. For how to create a super node, see [Creating Super Node](#create).

---

### How do I use EKS security groups?[](id:FAQ4)

When creating the elastic cluster Pod, if you do not specify a security group, the default security group will be used. You can also specify security group for the Pod through `Annotation eks.tke.cloud.tencent.com/security-group-id: security group ID`. Make sure that the security group ID already exists in the region where the workload resides. For more information on this annotation, see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).

---

### How do I set a container termination message?[](id:FAQ5)


Kubernetes can set the message source of the container exit through `terminationMessagePath`, that is, when a container exits, Kubernetes will retrieve the termination message from the termination message file specified in the `terminationMessagePath` field of the container, and use the message to populate the container termination message. The default value of the message is `/dev/termination-log`.

Moreover, you can set the `terminationMessagePolicy` field of a container for further termination message customization. This field defaults to `File`, which means the termination message is retrieved only from the termination message file. You can set it to `FallbackToLogsOnError` as needed, which means the last chunk of container log output will be used as the termination message if the container exits with an error and the termination message file is empty.

The sample code is as shown below:


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

---
### How do I use the `Host` parameter?[](id:FAQ6)

Note the following when using elastic clusters:

Elastic clusters do not have nodes but are compatible with `Host` parameters, such as `Hostpath`, `Hostnetwork: true`, and `DnsPolicy: ClusterFirstWithHostNet`.

Note that these parameters cannot deliver the full capabilities of K8s, as there is no node.

For example, you may want to use `Hostpath` to share data, but the two Pods scheduled to the same virtual node will see the `Hostpath` of different hosts. In addition, if the Pod is rebuilt, `Hostpath` files will be deleted at the same time.

---
### How do I mount CFS/NFS?[](id:FAQ7)

In elastic clusters, you can use Tencent Cloud's [Cloud File Storage (CFS)](https://intl.cloud.tencent.com/document/product/582/9127) or mount an external NFS as a volume to a Pod for persistent data storage. A sample YAML to mount CFS/NFS to a Pod is as shown below:

<dx-codeblock>
###  yaml
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
    ---
    </dx-codeblock>


- spec.volumes: Set the name, type, and parameters of the volume.
- spec.volumes.nfs: Set the NFS/CFS disk.
- spec.containers.volumeMounts: Set the mount point of the volume in the Pod.

For detailed directions of mounting a volume to a Pod, see [Instructions for Other Storage Volumes](https://intl.cloud.tencent.com/document/product/457/30678).


---
### How do I speed up container startup by image reuse?[](id:FAQ8)
EKS supports caching container images to speed up the next startup of the container with the same images.

**Conditions for reuse:**

1. For Pods with the same Workload, if a Pod is created and terminated at the same AZ within the cache time, the new Pod will not pull the same image by default.
2. If you want to reuse images for Pods with different Workloads (including Deployment, Statefulset, and Job), use the following annotation:
```
eks.tke.cloud.tencent.com/cbs-reuse-key
```
For the Pods with the same annotation value under the same user account, the start-up image will be reused within the cache time as much as possible. We recommend you enter the image name of the annotation value: **eks.tke.cloud.tencent.com/cbs-reuse-key: "image-name"**.

**Cache time:** 6 hours.


---
### Instructions for exceptional image reuse[](id:FAQ9)
When the image reuse feature is enabled and a Pod is created, `$kubectl describe pod` may encounter the following errors:
- `no space left on device: unknown`
- `Warning FreeDiskSpaceFailed 26m eklet, eklet-subnet-xxx failed to garbage collect required amount of images. Wanted to free 4220828057 bytes, but freed 3889267064 bytes`

**Solution:**
No action is required. Wait for a few minutes and the Pod will run automatically.

**Cause:**
- `no space left on device: unknown`
When the Pod reuses the system disk by default, the original image in the system disk occupies all of the space, and the disk does not have enough space to download the new image, so the error "no space left on device: unknown" is reported. EKS supports a regular image repossession mechanism, which, when the whole space is occupied, will automatically delete the existing redundant images in the system disk to free up the current disk (It takes several minutes).
- `Warning FreeDiskSpaceFailed 26m eklet, eklet-subnet-xxx failed to garbage collect required amount of images. Wanted to free 4220828057 bytes, but freed 3889267064 bytes`
This log shows that the current Pod needs 4220828057 bytes to download the image, but currently only 3889267064 bytes are available. The cause is that there are multiple images on the disk and only some images have been freed up. EKS's regular image repossession mechanism will continue to free up until a new image can be successfully pulled.



---
### What should I do if `Operation not permitted` is reported when I mount an external NFS[](id:FAQ10)

If you use an external NFS for persistent storage, the event `Operation not permitted` will be reported when a connection is made. You need to modify the `/etc/exports` file of your NFS and add the `/&lt;path&gt;&lt;ip-range&gt;(rw,insecure)` parameter. See example below:
```
/data/  10.0.0.0/16(rw,insecure)
```

---


### How do I free up a full Pod disk (ImageGCFailed)?

EKS Pods provide 20 GB of free system disk space by default. If the disk is full, you can free it up in the following ways.

#### 1. Free up unused container images 

If 80% of the space is used, the EKS backend will trigger the container image repossession process to recover the unused images and free up the space. If this fails, `ImageGCFailed: failed to garbage collect required amount of images` will be reported to remind you of the insufficient disk space.

Common causes of insufficient disk space include:
- The business has a lot of temporary outputs. You can confirm this with the `du` command.
- The business holds deleted file descriptors, so disk space is not freed up. You can confirm this with the `lsof` command.

If you want to adjust the threshold for the container image repossession, set the following annotation:
```
eks.tke.cloud.tencent.com/image-gc-high-threshold: "80"
```

#### 2. Clean up exited containers 

If your business has been upgraded in-place or a container has abnormally exited, the exited container will be retained until the disk utilization reaches 85%. The cleanup threshold can be adjusted with the following annotation:
```
eks.tke.cloud.tencent.com/container-gc-threshold: "85"
```
If you don't want to have the exited container automatically cleaned up (for example, you need the exit information for further troubleshooting), you can disable the automatic cleanup with the following annotation; however, the disk space cannot be automatically freed up in this case.
```
eks.tke.cloud.tencent.com/must-keep-last-container: "true"
```

>? This feature was launched on September 15, 2021 (UTC +8) and is not available on Pods created earlier.

#### 3. **Restart Pods with high disk usage**

You need to restart a Pod with the following annotation after the container's system disk usage exceeds a certain percentage:

```
eks.tke.cloud.tencent.com/pod-eviction-threshold: "85"
```

Only the Pod is restarted, but the host will not be rebuilt. Normal gracestop, prestop, and health checks are performed for the exit and startup.

>? This feature was launched on April 27, 2022 (UTC +8) and can be enabled on Pods created earlier only after they are rebuilt.



---

### 9100 port issue

EKS Pods expose monitoring data via port 9100 by default, and you can access 9100/metrics to get the data by running the following command:
- Get all metrics:
```
curl -g "http://<pod-ip>:9100/metrics" 
```
- We recommend you remove the `ipvs` metric for large clusters:
```
curl -g "http://<pod-ip>:9100/metrics?collect[]=ipvs"
```

If your business requires listening on port 9100, you can avoid conflicts by using other ports to collect monitoring data when creating a Pod. The configuration is as shown below:
```
eks.tke.cloud.tencent.com/metrics-port: "9110" 
```

If the port for monitoring data exposure is not changed and the business listens on port 9100 directly, an error will be reported in the new EKS network scheme, indicating that port 9100 is already in use:
```
listen() to 0.0.0.0:9100, backlog 511 failed (1: Operation not permitted)
```

When this error is reported, you need to add the annotation `metrics-port` to the Pod to change the monitoring port and then rebuild the Pod.

>! If the Pod has a public EIP, you need to set up a security group. Pay attention to port 9100 and open required ports.


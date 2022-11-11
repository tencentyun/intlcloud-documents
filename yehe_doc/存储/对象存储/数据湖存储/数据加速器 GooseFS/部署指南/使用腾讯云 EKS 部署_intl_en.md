 [Elastic Kubernetes Service (EKS)](https://intl.cloud.tencent.com/document/product/457/34040) is a TKE service mode that allows you to deploy workloads without purchasing any nodes. EKS is fully compatible with native Kubernetes, allowing you to purchase and manage resources natively. This service is billed based on the actual amount of resources used by containers. In addition, EKS provides extended support for Tencent Cloud products, such as storage and network products, and can ensure the secure isolation of containers. EKS is ready to use out-of-the-box.

Deploying GooseFS with Tencent Cloud EKS can make full use of the elastic computing resources from EKS and construct an on-demand, pay-as-you-go COS access acceleration service billed on a per second basis.

## Architecture

The figure below shows the general architecture of deploying GooseFS with Tencent EKS.
![](https://main.qcloudimg.com/raw/edccf984a806e02a53dd2f88a6fb4728.jpg)

As shown in the figure, the entire architecture consists of three parts: **EKS Managed Components**, **User Resource Pool**, and **COS Server**. **User Resource Pool** is mainly used to deploy GooseFS clusters, and **COS Server** is used as a remote storage system and can be replaced by CHDFS, a public cloud storage service. During the construction process:
- Both GooseFS Master and Worker are deployed as Kubernetes StatefulSet.
- Fluid is used to start a GooseFS cluster.
- Fuse Client is integrated into the sandbox of the User Pod.
- The usage method is the same as standard Kubernetes.

## Directions

### Preparing the environment

1. Create an EKS cluster. For directions, see [Creating a Cluster](https://intl.cloud.tencent.com/document/product/457/34048).
2. Enable cluster access and select internet access or private network access as appropriate. Refer to [Connecting to a Cluster](https://intl.cloud.tencent.com/document/product/457/34049) for directions.
3. Run the `kubectl get ns` command to make sure the cluster is available:
<dx-codeblock>
::: shell shell
   -> goosefs kubectl get ns
   NAME              STATUS   AGE
   default           Active   7h31m
   kube-node-lease   Active   7h31m
   kube-public       Active   7h31m
   kube-system       Active   7h31m
:::
</dx-codeblock>
4. Obtain `helm`. Refer to [Helm docs](https://helm.sh/docs/intro/install/#from-the-binary-releases) for directions.

### Installing GooseFS 

1. Enter the `helm install` command to install a chart package and Fluid:
<dx-codeblock>
::: shell shell
   -> goosefs helm install fluid ./charts/fluid-on-tke
   NAME: fluid
   LAST DEPLOYED: Tue Jul  6 17:41:20 2021
   NAMESPACE: default
   STATUS: deployed
   REVISION: 1
   TEST SUITE: None
:::
</dx-codeblock>
2. View the status of pods related to `fluid`:
<dx-codeblock>
::: shell shell
   -> goosefs kubectl -n fluid-system get pod
   NAME                                         READY   STATUS    RESTARTS   AGE
   alluxioruntime-controller-78877d9d47-p2pv6   1/1     Running   0          59s
   dataset-controller-5f565988cc-wnp7l          1/1     Running   0          59s
   goosefsruntime-controller-6c55b57cd6-hr78j   1/1     Running   0          59s
:::
</dx-codeblock>
3. Create a `dataset`, modify the relevant variables as appropriate, and run the `kubectl apply -f dataset.yaml` command to apply the `dataset`:
<dx-codeblock>
::: yaml yaml
   apiVersion: data.fluid.io/v1alpha1
   kind: Dataset
   metadata:
     name: ${dataset-name}
   spec:
     mounts:
     - mountPoint: cosn://${bucket-name}
       name: ${dataset-name}
       options:
         fs.cosn.userinfo.secretKey: XXXXXXX
         fs.cosn.userinfo.secretId: XXXXXXX
         fs.cosn.bucket.region: ap-${region}
         fs.cosn.impl: org.apache.hadoop.fs.CosFileSystem
         fs.AbstractFileSystem.cosn.impl: org.apache.hadoop.fs.CosN
         fs.cos.app.id: ${user-app-id}
:::
</dx-codeblock>
4. Create a `GooseFS` cluster with yaml below, and run `kubectl apply -f runtime.yaml`:
<dx-codeblock>
::: yaml yaml
    apiVersion: data.fluid.io/v1alpha1
    kind: GooseFSRuntime
    metadata:
      name: slice1
      annotations:
        master.goosefs.eks.tencent.com/model: c6
        worker.goosefs.eks.tencent.com/model: c6
    spec:
      replicas: 6 # Number of workers. Although the controller can be expanded, GooseFS currently does not support automatic data re-balance.
      data:
        replicas: 1 # Number of GooseFS data replicas
      goosefsVersion:
        imagePullPolicy: Always
        image: ccr.ccs.tencentyun.com/cosdev/goosefs   # Image and version of a GooseFS cluster
        imageTag: v1.0.1
      tieredstore:
        levels:
          - mediumtype: MEM # Supports MEM, HDD, and SSD, which represent memory, premium cloud storage, and SSD cloud storage respectively.
            path: /data
            quota: 5G   # Both memory and cloud storage will take effect. The minimum capacity of cloud storage is 10 GB.
            high: "0.95"
            low: "0.7"
      properties:
        goosefs.user.streaming.data.timeout: 5s
        goosefs.job.worker.threadpool.size: "22"
        goosefs.master.journal.type: UFS        # UFS or EMBEDDED. UFS for the case of only one master.
    #    goosefs.worker.network.reader.buffer.size: 128MB
        goosefs.user.block.size.bytes.default: 128MB
    #    goosefs.user.streaming.reader.chunk.size.bytes: 32MB
    #    goosefs.user.local.reader.chunk.size.bytes: 32MB
        goosefs.user.metrics.collection.enabled: "false"
        goosefs.user.metadata.cache.enabled: "true"
        goosefs.user.metadata.cache.expiration.time: "2day"
      master:
        # A required parameter, which sets the VM specification of pods. Default value: 1c1g
        resources:
          requests:
            cpu: 8
            memory: "16Gi"
          limits:
            cpu: 8
            memory: "16Gi"
        replicas: 1
    #    journal:
    #      volumeType: pvc
    #      storageClass: goosefs-hdd
        jvmOptions:
          - "-Xmx12G"
          - "-XX:+UnlockExperimentalVMOptions"
          - "-XX:ActiveProcessorCount=8"
          - "-Xms10G"
      worker:
        jvmOptions:
          - "-Xmx28G"
          - "-Xms28G"
          - "-XX:+UnlockExperimentalVMOptions"
          - "-XX:MaxDirectMemorySize=28g"
          - "-XX:ActiveProcessorCount=8"
        resources:
          requests:
            cpu: 16
            memory: "32Gi"
          limits:
            cpu: 16
            memory: "32Gi"
      fuse:
        jvmOptions:
          - "-Xmx4G"
          - "-Xms4G"
          - "-XX:+UseG1GC"
          - "-XX:MaxDirectMemorySize=4g"
          - "-XX:+UnlockExperimentalVMOptions"
          - "-XX:ActiveProcessorCount=24"
:::
</dx-codeblock>
5. Check the statuses of the cluster and PVC:
<dx-codeblock>
::: shell shell
   -> goosefs kubectl get pod
   NAME              READY   STATUS    RESTARTS   AGE
   slice1-master-0   2/2     Running   0          8m8s
   slice1-worker-0   2/2     Running   0          8m8s
   slice1-worker-1   2/2     Running   0          8m8s
   slice1-worker-2   2/2     Running   0          8m8s
   slice1-worker-3   2/2     Running   0          8m8s
   slice1-worker-4   2/2     Running   0          8m8s
   slice1-worker-5   2/2     Running   0          8m8s
   -> goosefs kubectl get pvc
   slice1 Bound default-slice1 100Gi ROX fluid 7m37s       # PVC and dataset share the same name. 100Gi is a dummy value used as a placeholder.
:::
</dx-codeblock>


### Loading data
To preload data, you only need to create a resource with the yaml below (e.g. `kubectl apply -f dataload.yaml`). A response example after running is as follows:
```
   apiVersion: data.fluid.io/v1alpha1
   kind: DataLoad
   metadata:
     name: slice1-dataload
   spec:
     # Configuring the dataset that needs to load data
     dataset:
       name: slice1
       namespace: default
```

After creating, you can check the status via `kubectl get dataload slice1-dataload`.

### Mounting PVC to a service pod

The user service container should be used in accordance to the K8s instruction. Refer to [Kubernetes documentation](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) for details.

### Terminating a GooseFS cluster

To terminate a GooseFS cluster, you can specify the master and worker nodes to be deleted and run the `delete` command. **This is a high-risk operation. Make sure that there is no I/O operation on GooseFS in the service pod.**
```
   -> goosefs kubectl get sts
   NAME            READY   AGE
   slice1-master   1/1     14m
   slice1-worker   6/6     14m
   -> goosefs kubectl delete sts slice1-master slice1-worker
   statefulset.apps "slice1-master" deleted
   statefulset.apps "slice1-worker" deleted
```

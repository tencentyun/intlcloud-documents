This document describes the annotation that is unique to super nodes and effective for Pods running on super nodes in TKE general and Serverless clusters.

## Annotation Usage
### Adding a Pod annotation to a workload
Annotations in this document are at the Pod level. Usually, it is the workload not bare Pod that is used by users. This document describes how to add a Pod annotation to a Deployment. Note that a Pod annotation is added in the `.spec.template.metadata.annotations` field of a workload.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
      annotations:
        eks.tke.cloud.tencent.com/retain-ip: 'true' # A Pod annotation is added in the `.spec.template.metadata.annotations` field of a workload.
    spec:
      containers:
      - name: nginx
        image: nginx
```


### Global configuration
You can modify the global configuration to make an annotation effective for all Pods in a cluster by default, that is, the `eks-config` ConfigMap in the `kube-system` namespace. If there are no such configurations, create one.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: eks-config
  namespace: kube-system
data:
  pod.annotations: |
    eks.tke.cloud.tencent.com/resolv-conf: |
      nameserver 183.60.83.19 
    eks.tke.cloud.tencent.com/host-sysctls: '[{"name": "net.core.rmem_max","value": "26214400"}]'
```

>? Annotations added to Pods take priority over the global configuration.

## Resources and Specifications

### Specifying the CPU and memory

By default, Pods running on super nodes automatically calculate the specifications of underlying resources according to the request and limit values. You can also specify the computing resource specifications required by Pods by adding Pod annotations. For more information, see [Specifying resource specifications](https://intl.cloud.tencent.com/document/product/457/36161).

```yaml
eks.tke.cloud.tencent.com/cpu: '8'
eks.tke.cloud.tencent.com/mem: '16Gi' # The memory needs to be measured in Gi. If G is used, parameter errors will be reported.
```


### Specifying system disk size

A Pod running on a super node provides 20 GB of free system disk size by default. The system disk has the same lifecycle as the Pod, meeting the requirements for system disk resources in general scenarios. If you need a larger system disk size, you can use the annotation to declare the desired size. Note that the excessive part will be billed based on the pay-as-you-go published price of a CBS Premium Cloud Storage cloud disk. For billing details, see [Pricing | Cloud Block Storage](https://buy.intl.cloud.tencent.com/price/cbs). Below is a sample annotation of the system disk size:
```yaml
eks.tke.cloud.tencent.com/root-cbs-size: '50'  # Specify the system disk size. Additional charges are applied for the part of the size exceeding 20 Gi
```
>? For detailed instructions on how to adjust the disk size when using the image cache, see [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).

### Automatically upgrading the specification

Pods on super nodes automatically calculate the specifications of underlying resources according to the request and limit values. If no such resources exist, Pod creation will fail and the system will prompt that the resources are insufficient. If you agree to create a Pod with higher-specced resources, add the following annotation to the Pod to enable automatic specification upgrade. Fees will be charged according to the upgraded specifications.

```yaml
eks.tke.cloud.tencent.com/spec-auto-upgrade: 'true' # When resources are insufficient, enable automatic specification upgrade, which is performed only once according to the CPU specifications.
```

### Specifying the GPU

To specify the GPU, add the following annotation to the Pod:

```yaml
eks.tke.cloud.tencent.com/gpu-type: 'T4,V100' # Specify the GPU model by priority. If you use the 1/4 T4 vGPU, specify it as 1/4*T4.
```
>? You need to set the number of cards and specification of the GPU in `Request` and `Limit` based on your GPU model. For more information, see [Resource Specifications](https://intl.cloud.tencent.com/document/product/457/34057).


### Specifying the CPU type
To specify the CPU type, add the following annotation to the Pod:


```yaml
eks.tke.cloud.tencent.com/cpu-type: 'amd,intel' # It indicates that AMD resource Pods are created first. If the AMD resources in the AZ of the selected region are insufficient, Intel resource Pods are created.
```

### Enabling the spot mode
To enable the [spot mode](https://intl.cloud.tencent.com/document/product/457/46967), add the following annotation to the Pod:

```yaml
eks.tke.cloud.tencent.com/spot-pod: 'true'
```

## IP Retention and EIP

### Fixing an IP in StatefulSet

You can use a fixed IP if the workload is StatefulSet or a bare Pod is used (note that you cannot change the Pod name). You can add the Pod annotation to enable the fixed IP:

```yaml
eks.tke.cloud.tencent.com/retain-ip: 'true' # Set the value to `true` to enable the fixed IP.
eks.tke.cloud.tencent.com/retain-ip-hours: '48' # The maximum IP retention period in hours. If a terminated Pod is not created after this period, the IP will be released.
```

>? You don't need to add annotations to use the fixed IP for super nodes in the TKE cluster.

### Binding an EIP
To bind an EIP, add the following annotation to the Pod:

```yaml
eks.tke.cloud.tencent.com/eip-attributes: '{"InternetMaxBandwidthOut":50, "InternetChargeType":"TRAFFIC_POSTPAID_BY_HOUR"}' # The value can be an empty string, indicating that the EIP is enabled and the default configuration is used. You can also use the JSON parameter used to create the EIP API. For more information on the parameter list, visit https://cloud.tencent.com/document/api/215/16699#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0. In this example, the parameter indicates that the EIP is pay-as-you-go and the bandwidth cap is 50 Mbps.
```

>! An EIP cannot be bound for non-bill-by-IP accounts (traditional accounts). If you are using a non-bill-by-IP account, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for account upgrade.



### Fixing an EIP in StatefulSet
To fix an EIP in StatefulSet, add the following annotation to the Pod:


```yaml
eks.tke.cloud.tencent.com/eip-attributes: '{}' # Enable the EIP and use the default configuration.
eks.tke.cloud.tencent.com/eip-claim-delete-policy: 'Never' # It indicates whether to repossess the EIP after the Pod is deleted. By default, it is repossessed. `Never` indicates not to repossess, which means the same EIP will be bound to the next Pod created under the same name, thereby fixing the EIP.
```

>! When `Never` is set for Deployment workloads, the EIP will not be repossessed after the Pod is deleted or used for the roll-updated Pod.

### Using an existing EIP in StatefulSet

To bind an existing EIP to the Pod instead of automatically creating one, specify the ID of the EIP instance to be bound to the Pod. The annotation is as follows:

```yaml
eks.tke.cloud.tencent.com/eip-id-list: 'eip-xx1,eip-xx2' # Specify the list of existing EIP instances and make sure that the number of Pod replicas in StatefulSet is less than or equal to that of EIP instances.
```

>! When specifying the EIP, do not configure the `eip-attributes` annotation.

## Image and Registry

### Ignoring the certificate verification

If the certificate of the self-built image registry is self-signed, the image pull will fail (ErrImagePull). You can add the following annotation to the Pod to specify not to verify the certificate when images are pulled from the image registry:

```yaml
eks.tke.cloud.tencent.com/registry-insecure-skip-verify: 'harbor.example.com' # You can write multiple ones separated by comma.
```

### Using the HTTP protocol

If HTTP rather than HTTPS is used by the self-built image registry, the image pull will fail (ErrImagePull). You can add the following annotation to the Pod to use HTTP when images are pulled from the image registry:

```yaml
eks.tke.cloud.tencent.com/registry-http-endpoint: 'harbor.example.com' # You can write multiple ones separated by comma.
```

### Reusing an image

By default, the system disk is reused on super nodes to speed up the startup, specifically, the system disk of the Pod within the caching period (two hours after termination) in the same AZ of the same workload. To reuse Pod images in different workloads, add the same `cbs-reuse-key` annotation to all of them:

```yaml
eks.tke.cloud.tencent.com/cbs-reuse-key: 'image-name'
```

### Image cache

Super nodes provide [image cache capabilities](https://intl.cloud.tencent.com/document/product/457/44484), where an image cache instance is created in advance, the target image is automatically downloaded, and the cloud disk snapshot is created. Then you can enable the image cache when creating a Pod. The snapshot of the image cache instance is automatically matched by image name, allowing you to use the snapshot image content and saving the need to download the image a second time, thereby speeding up the startup.

The annotation to enable the image cache is as follows:

```yaml
eks.tke.cloud.tencent.com/use-image-cache: 'auto'
```

Specify the type of cloud disk created with the image cache:

```yaml
eks.tke.cloud.tencent.com/image-cache-disk-type: 'CLOUD_SSD'  # Specify the type of cloud disk created with the image cache. Valid values: `CLOUD_BASIC` (HDD cloud disk), `CLOUD_PREMIUM` (Premium Cloud Disk, it is the default value), `CLOUD_SSD` (SSD), `CLOUD_HSSD` (Enhanced SSD), `CLOUD_TSSD` (ulTra SSD).
```


Specify the size of cloud disk created with the image cache:

```yaml
eks.tke.cloud.tencent.com/image-cache-disk-size: '50' # Specify the size of cloud disk created with the image cache. The default size is the one set when the cloud disk was created. The size can only be increased, but cannot be decreased.
```

You can choose to manually specify the image cache instance instead of having it automatically matched:

```yaml
eks.tke.cloud.tencent.com/use-image-cache: 'imc-xxx'
```

The data disk created by the image cache is terminated upon Pod deletion, but you can specify a period to retain it by using an annotation. When retention is enabled, the retained data disk will be reused when the next Pod is created, saving the time to roll the data from the snapshot to the new cloud disk:

```yaml
eks.tke.cloud.tencent.com/image-cache-disk-retain-minute: '10' # Specify to retain the data disk created by the image cache for 10 minutes after Pod termination.
```

## Binding a Security Group

By default, super nodes bind Pods to the `default` security group in the default project in the same region. You can also specify a security group by adding the following annotation to the Pod:

```yaml
eks.tke.cloud.tencent.com/security-group-id: 'sg-id1,sg-id2' # Enter the IDs of the security groups in the region and separate them by comma. Network policies take effect based on the sequence of security groups. By default, a security group can be bound to up to 2,000 Pods. To increase this limit, submit a ticket for application.
```

## Binding a Role

By default, super nodes associate Pods with the `TKE_QCSLinkedRoleInEKSLog` role and grant log collection components in the Pods the permission to report logs. You can associate Pods with other CAM roles by using the annotation to get permissions to manipulate Tencent Cloud resources.

```yaml
eks.tke.cloud.tencent.com/role-name: 'TKE_QCSLinkedRoleInEKSLog'
```

## Setting the Host Kernel Parameters

Some kernel parameters are isolated by network namespace and cannot be viewed or set in containers. A Pod on the super node exclusively occupies a VM, but this doesn't mean that you can set host kernel parameters in containers.

You can add Pod annotations to set host kernel parameters:

```yaml
eks.tke.cloud.tencent.com/host-sysctls: '[{"name": "net.core.rmem_max","value": "26214400"},{"name": "net.core.wmem_max","value": "26214400"},{"name": "net.core.rmem_default","value": "26214400"},{"name": "net.core.wmem_default","value": "26214400"}]'
```

## Loading the Kernel Module
To load the [TOA kernel module](https://intl.cloud.tencent.com/document/product/608/18945), add the following annotation to the Pod:

```yaml
eks.tke.cloud.tencent.com/host-modprobe: 'toa'
```

## Automatic Recreation and Failover

An agent inside the VM in the cluster of the super node reports heartbeats to the control plane. Generally speaking, if the report times out (five minutes by default), the process in the Pod fails due to a high load. In this case, the cluster migrates the VM by default for failover (the current VM is shut down and a new one is created automatically to take over the Pod).

If you don't want to have another one automatically created (so that the problematic environment can be retained), then add the following annotation to the Pod:

```yaml
eks.tke.cloud.tencent.com/recreate-node-lost-pod: "false"
```

To remove the abnormal Pod traffic in less time than the default five minutes, add the following annotation to the Pod to customize the heartbeat timeout period:

```yaml
eks.tke.cloud.tencent.com/heartbeat-lost-period: 1m 
```

## Disk Cleanup

When the disk usage on the super node becomes too high, a cleanup process is automatically triggered to release the space. You can view the disk usage through `df -h`.

Common causes of insufficient disk space include:
- The business has a lot of temporary outputs. You can confirm this with the `du` command.
- The business holds deleted file descriptors, so disk space is not freed up. You can confirm this with the `lsof` command.

### Cleaning up a container image

By default, if the disk usage reaches 80%, the container image is automatically cleaned up to free up the space. If no container images can be released, the following event is reported:

```txt
failed to garbage collect required amount of images. Wanted to free 7980402688 bytes, but freed 0 bytes
```

To customize the cleanup threshold, add the following annotation to the Pod: 

```yaml
eks.tke.cloud.tencent.com/image-gc-high-threshold: '80' # When the disk usage reaches 80%, image cleanup is triggered.
eks.tke.cloud.tencent.com/image-gc-low-threshold: '75' # After triggered, the container image cleanup stops when 5% (high-threshold - low-threshold) of the space is released.
eks.tke.cloud.tencent.com/image-gc-period: '3m' # The disk space is checked once every three minutes by default.
```

### Cleaning up an exited container

If your business has been upgraded in-place or a container has abnormally exited, the exited container will be retained until the disk utilization reaches 85%. The cleanup threshold can be adjusted with the following annotation:

```yaml
eks.tke.cloud.tencent.com/container-gc-threshold: "85"
```

If you don't want to have the exited container automatically cleaned up (for example, you need the exit information for further troubleshooting), you can disable the automatic cleanup with the following annotation; however, the disk space cannot be automatically freed up in this case.

```yaml
eks.tke.cloud.tencent.com/must-keep-last-container: "true"
```

### Restarting the Pods with high disk usage

You need to restart a Pod with the following annotation after the container's system disk usage exceeds a certain percentage:

```yaml
eks.tke.cloud.tencent.com/pod-eviction-threshold: "85" # This feature is enabled after set. It is not enabled by default.
```

Only the Pod is restarted, but the host will not be rebuilt. Normal gracestop, prestop, and health checks are performed for the exit and startup.

>! This feature was launched on April 27, 2022 (UTC +8). The Pods created before that date must be rebuilt to enable the feature.

## Monitoring Metrics

### 9100 port issue

Pods on super nodes expose monitoring data via port 9100 by default, and you can access 9100/metrics to get the data by running the following command:

- Get all metrics:
  ```bash
  curl -g "http://<pod-ip>:9100/metrics"
  ```

- We recommend you remove the `ipvs` metric for large clusters:
  ```bash
  curl -g "http://<pod-ip>:9100/metrics?collect[]=ipvs"
  ```

If the business listens on port 9100, the following error will be reported, indicating that port 9100 has been used:

```
listen() to 0.0.0.0:9100, backlog 511 failed (1: Operation not permitted)
```

You can customize the port number to be used for exposing monitoring data to avoid business conflicts. The configuration method is as follows:

```yaml
eks.tke.cloud.tencent.com/metrics-port: "9110"
```

>? If the Pod has a public EIP, you need to set up a security group. Pay attention to port 9100 and open required ports.

### Monitoring data reporting frequency

The `cAdvisor` monitoring data exposed on the super node is refreshed once every 30s by default. You can adjust the refresh frequency with the following annotation:

```yaml
eks.tke.cloud.tencent.com/cri-stats-interval: '30s'
```

### Customizing the monitoring metric path

By default, monitoring data is exposed through the `/metrics` path, which doesn't need to be changed. To customize it, use the following annotation:

```yaml
eks.tke.cloud.tencent.com/custom-metrics-url: '/metrics'
```

## Naming the Pod ENI

By default, a Pod uses the `eth0` ENI. To rename the ENI, add the following annotation:

```yaml
internal.eks.tke.cloud.tencent.com/pod-eth-idx: '1' # Name the ENI `eth1`. 
```

## Custom DNS

By default, the host of the Pod uses the DNS of `183.60.83.19` and `183.60.82.98` in the VPC. To modify it, configure the following annotation:

```yaml
eks.tke.cloud.tencent.com/resolv-conf: |
  nameserver 4.4.4.4
  nameserver 8.8.8.8
```

>! A custom DNS on the host prevails.

## Collecting Logs to Kafka

Super nodes allow you to use open-source log collection components to collect logs to Kafka. If files in containers are collected or [multi-line merging](https://intl.cloud.tencent.com/document/product/457/40216) is used during collection, you need to properly configure the line size that defaults to 2 MB. If it exceeds 2 MB, the log in the line is discarded. The line size can be adjusted with the following annotation:

```yaml
internal.eks.tke.cloud.tencent.com/tail-buffer-max-size: '2M' # A single-line log with the maximum size of 2M is supported by default.
```

When logs are collected to Kafka, the field of the log content is `log`. To configure it to `message`, use the following annotation:

```yaml
eks.tke.cloud.tencent.com/log-key-as-message: 'true'
```

When reported, logs contain the Pod metadata information, which is put in the `kubernetes` field as a `string`. To set it to the `json` format, configure the following annotation:

```yaml
eks.tke.cloud.tencent.com/filebeat-metadata-format: 'true'
```

## Delaying the Termination

When a job running on the super node ends, the underlying resources along with the temporary output are terminated. If you run kubectl logs <pod>, "can not found connection to pod" will be reported. To retain underlying resources for problem locating, delay the termination with the following configuration:

```yaml
eks.tke.cloud.tencent.com/reserve-sandbox-duration: '1m' # Enable the feature to delay the termination for one minute. When the last container of the Pod in the `Failed` status exits, the underlying resources are retained for one minute.
eks.tke.cloud.tencent.com/reserve-succeeded-sandbox: 'false' # Termination delay only applies to Pods in the `Failed` status. You can also change the field to apply it to Pods in the `Succeeded` status.
eks.tke.cloud.tencent.com/reserve-task-shorter-than: '5s' # If you only care about short-running jobs, you can configure this parameter. Then the termination delay will be triggered only when any container in the Pod runs shorter than the specified value. This parameter is not enabled by default.
```

## Service Rule Sync

### Disabling the service rule sync

The cluster of the super node generates K8s service rules through IPVS. If you don't need such service rules, you can disable them with the following annotation:

```yaml
eks.tke.cloud.tencent.com/cluster-ip-switch: 'disable'
```

>! After service rules are disabled, service discovery in all clusters becomes invalid. `dnsPolicy` of `ClusterFirst` cannot be used by the Pod, and you need to change it to another type such as `Default`.

### Waiting for the service rule sync

The cluster syncs service rules when the Pod is started. To wait for the sync to be completed before starting the Pod, use the following configuration:

```yaml
eks.tke.cloud.tencent.com/duration-to-wait-service-rules: '30s' # Wait for the service rule sync to be completed before starting the Pod. The maximum value of 30s is set here.
```

### Setting the IPVS parameter

IPVS rules can be controlled with the following annotation:

```yaml
eks.tke.cloud.tencent.com/ipvs-scheduler: 'sh' # Scheduling algorithm. `sh` refers to source hash. Forwarding based on the source address hash facilitates distributed global loading balancing. The default value is `rr` (round robin).
eks.tke.cloud.tencent.com/ipvs-sh-port: "true" # Source hash is performed by port, which is valid only when `ipvs-scheduler` is `sh`.
eks.tke.cloud.tencent.com/ipvs-sync-period: '30s' # The maximum interval for refreshing rules, which defaults to 30s.
eks.tke.cloud.tencent.com/ipvs-min-sync-period: '2s' # The minimum interval for refreshing rules. By default, rules are refreshed upon service changes. You can modify this parameter to avoid frequent refreshes.
```


- Set not to guide the traffic through IPVS when the VIP of a CLB instance is accessed within the cluster.
It applies to guiding traffic through CLB but not IPVS for access within the cluster. When the annotation is configured for the service, no corresponding IPVS rules will be generated:
```yaml
service.cloud.tencent.com/discard-loadbalancer-ip: 'true' # The annotation is configured for the service and takes effect immediately without Pod rebuild required.
```


## Customizing the Pod Time Zone

By default, UTC time is used for Pods on super nodes. To adjust the time zone to UTC +8, add the following annotation:
```yaml
eks.tke.cloud.tencent.com/host-timezone: 'Asia/Shanghai' # This annotation is used to set the Pod time zone to UTC +8.
```

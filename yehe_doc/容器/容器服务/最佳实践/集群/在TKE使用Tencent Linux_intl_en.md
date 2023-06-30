

The underlying layer of a container realizes many features dependent on the kernel, such as the overlay system, namespace, and cgroup. Therefore, the features and stability of the kernel determine, to a great extent, the features and stability of the entire container PaaS platform. Tencent Linux is the official Linux version run by Tencent. You can learn about Tencent Linux and its use from this document.


## Tencent Linux Overview
Tencent Linux is maintained by Tencent’s kernel and virtualization team. Tencent Linux 2.4 is based on CentOS 7, and its user-state software package maintains compatibility with CentOS 7, the latest version. The software package of CentOS 7 can be directly used in Tencent Linux 2.4.

## Tencent Linux Kernel Version
Tencent Linux 2.4 currently uses kernel 4.14, and the [code and rpm package](https://github.com/Tencent/TencentOS-kernel) can be obtained.

## Differences Between Tencent Linux and CentOS
The key difference lies in the kernel versions, such as the minimum adjustment of the user state and the configuration of the YUM source. For more information, see [Tencent Linux](https://intl.cloud.tencent.com/document/product/213/32485).

## Relationship Between Tencent Linux and TKE Optimized Images
Tencent Linux and TKE Optimized images have the same kernel, but Tencent Linux 2.4 uses the public images of Tencent CVMs, whereas TKE Optimized images are from the image marketplace.

TKE will use `Tencent Linux2.4` to replace `CentOS 7.6 TKE Optimized` and `Ubuntu18.04 TKE Optimized`. Clusters that currently use `CentOS 7.6 TKE Optimized` and `Ubuntu18.04 TKE Optimized` can continue to use them, but newly created clusters will no longer support the images of the above two OS versions. You can refer to the directions in [Modifying the OS](#revise) to switch the OS image of newly created nodes in the cluster to `Tencent Linux2.4`.

## Advantages of Tencent Linux
Compared with released versions such as CentOS and Ubuntu, Tencent Linux mainly has the following advantages:
- It has been extensively verified and refined over the years by use in Tencent’s internal services.
- It has the support of a world-class kernel expert team.
- It includes some key performance optimization and customized features for container scenarios.

### Internal service verification and refinement

Since the launch of R&D for the project in 2010, Tencent Linux has been used within Tencent for 10 years, with millions of deployments. Tencent Linux accounts for 99% of Tencent’s internal Linux systems, covering all Tencent services. Tencent has the most diverse range of services in China, including social media, games, financial payment, AI, and security services. Therefore, it has strict requirements on the underlying OS, including in terms of stability, performance, and compatibility.
In container scenarios, many of Tencent’s core services have been partially or completely containerized. For example, the logical service of WeChat has been completely containerized. Then, based on the service features of WeChat, we made a series of optimizations, such as to ensure the smooth operation of WeChat during the peak hours of red packet delivery over the annual Spring Festival. Meanwhile, the Tencent Linux team works closely with WeChat to provide data security solutions.

### Support by a kernel expert team

Currently, there are more than 30 full-time kernel experts providing support for kernel versions, including kvm maintenance experts and many other experts for subsystems such as kernel networks, storage, cgroup, and scheduling.
The strength of this support is also reflected in the frequency of version updates and hot patch release. From July to October, the Tencent Linux kernel 4.14 series released five versions. For more information, see [Version Records](https://github.com/Tencent/TencentOS-kernel/releases). Most of the issues encountered in Tencent’s internal services and by Tencent Cloud’s external clients can be located and fixed in a timely manner. Tencent Linux provides kernel hot patches to fix certain key issues online. Hot patches can be installed and take effect without the need to restart the device. Moreover, the latency SLA for users’ business can be improved due to the avoidance of business interruptions. Tencent Linux provides a complete hot patch solution for vulnerability fixes, including application-level hot patches and kernel-level hot patches. Tencent Linux releases more than 100 hot patches every year and provides fixes for most vulnerabilities within one week.

### Performance optimization

Based on the issues encountered by internal and external users in large-scale practice, Tencent Linux has made numerous performance optimizations for container scenarios, including the following:
1. Fixed exceptions caused by the reuse of connections in high-concurrency scenarios in IPVS mode ([#81775](https://github.com/kubernetes/kubernetes/issues/81775)).
2. Fixed network glitches caused by excessive IPVS rules under high-configuration nodes (with many cores) in IPVS mode.
3. <span id="three"></span>Fixed network glitches caused when cAdvisor is stuck in the kernel state for too long while reading memcg in high-density container scenarios (where the number of containers on a single node is large).
4. Fixed network glitches caused by CPU load balancing in scenarios of high-configuration nodes (with many cores) and large pods (which occupy many cores with high usage per core).
5. Fixed periodic network jitter caused by TCP connection monitoring (for example, the cAdvisor configuration is deployed separately to monitor TCP connections) in high-concurrency scenarios.
6. Optimized soft interruption when receiving network packages to enhance network performance.

The optimizations for the above container scenarios have been very effective. For example, with regard to [Issue 3](#three), the effect of ping latency monitoring is shown in the figure below (the part after 11:00 shows the effect after optimization):
!['image.png'](https://main.qcloudimg.com/raw/ac2cd0103df4c893070ea4f0169e4ab1.png)


### Customized container features
#### Display of container resources in isolation
The efficient running of many Golang and Java programs depends on correctly obtaining available CPU and memory resources of processes. However, in the containers of these programs, the resources obtained are the CPU and memory resources of nodes, which do not match the actual resources allocated by containers. This often results in invalid parameters, such as process thread pool parameters, leading to further problems.
The common solution in the community is to deploy FUSE to provide LXCFS to isolate the display of resources, such as `/proc/cpuinfo` and `/proc/meminfo`, by container. This solution requires nodes to be deployed in the LXCFS file system, and you also need to insert relevant volume and mount target configurations in POD sepc. For more information, see [Kubernetes Demystified: Using LXCFS to Improve Container Resource Visibility](https://dzone.com/articles/kubernetes-demystified-using-lxcfs-to-improve-cont).
Tencent Linux implements a similar LXCFS feature in its kernel. This means you do not need to deploy nodes in the LXCFS file system or modify POD spec. Instead, you simply need to run the following command to enable a global switch on nodes. Then, the information obtained by reading files such as `/proc/cpuinfo` and `/proc/meminfo` in containers will be displayed in isolation by container.
```
sysctl -w kernel.stats_isolated=1
```
In addition, considering that there are some special containers, such as the node monitoring component, for which node-level information may need to be read, Tencent Linux added a container-level switch `kernel.container_stats_isolated`. When the host-level switch is enabled, you only need to run the following command in the container launch script to disable the container-level switch. Then, the information obtained by reading files such as `/proc/cpuinfo` and `/proc/meminfo` in containers will be the host information.
```
sysctl -w kernel.container_stats_isolated=0
```
>! The container-level switch must be set in the container. Otherwise, it will not take effect for the container. For more information, see [Isolation of Information in Containers, Such as CPU, Memory, Processes, and Disks](https://github.com/Tencent/TencentOS-kernel/wiki/container-resource-view-isolation).

#### Isolation of more kernel parameters
- net.ipv4.tcp_max_orphans
- net.ipv4.tcp_workaround_signed_windows
- net.ipv4.tcp_rmem
- net.ipv4.tcp_wmem
- vm.max_map_count

The above kernel parameters often need to be customized and modified for business purposes, but the community kernel does not isolate these parameters by namespace. As a result, if a container modifies the above parameters, the modification will take effect for the host and all other containers. To meet the requirements of internal and external clients, Tencent Linux isolates these kernel parameters by namespace, so that you can customize these parameters in your container based on your needs without worrying about affecting other businesses.

#### Optimization of default container kernel parameters
In high-concurrency situations, packet loss may occur when a semi-connected queue is full. You can mitigate this issue by increasing the value of `net.core.somaxconn`. However, the default value of `net.core.somaxconn` in the container network namespace is only 128, and the code cannot be changed. In the Tencent Linux kernel, the default value has been adjusted to 4096 to prevent packet loss caused by a full semi-connected queue in high-concurrency situations.

 ## Directions
To use the Tencent Linux operating system in TKE cluster nodes, you need to select the `Tencent Linux` operating system on the basic information page of the cluster when [creating a cluster](https://intl.cloud.tencent.com/document/product/457/30637), as shown in the figure below:
![](https://main.qcloudimg.com/raw/6a3903f649a0cc7d8c8b065f89673cc7.png)

>! Besides supporting common CVM models, Tencent Linux also supports CPM and Nvidia GPU models.

## Relevant Operations

<span id="revise"></span>
### Modifying the OS
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2) and click **Cluster** in the left sidebar.
2. Click the ID of the cluster for which you want to modify the OS to go to the "Basic Information" page of the cluster.
3. In the node and network information module on the "Basic Information" page of the cluster, click ![](https://main.qcloudimg.com/raw/3b38ca6981068a10b031df5708bc4f41.png) to the right of the default OS, as shown in the figure below:
![](https://main.qcloudimg.com/raw/6b4275b89682eb272e930e7175d27b9a.png)
4. In the pop-up window, select **Tencent Linux 2.4 64bit** and click **Submit** to complete modification of the OS, as shown in the figure below:
![](https://main.qcloudimg.com/raw/58c072fc96c864b4a8a9484dd3b28147.png)



## References

- [Tencent Linux Official Documentation](https://intl.cloud.tencent.com/document/product/213/32485)
- [Tencent Linux Kernel Code](https://github.com/Tencent/TencentOS-kernel)
- [Container Resource View Isolation](https://github.com/Tencent/TencentOS-kernel/wiki/container-resource-view-isolation)

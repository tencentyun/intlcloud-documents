## Overview
This document describes how to configure the persistent memory for an M6p instance.


## Instance Configuration
This document uses a CVM instance with the following configuration. The obtained relevant information shall be subject to the actual conditions.
 - **Instance specification**: MEM Optimized M6p instance M6p.LARGE16 (4C16G). For the configuration of other specifications, see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).
 - **OS**: TencentOS Server 3.1 (TK4).
<dx-alert infotype="explain" title="">
Recommended configurations:
 - TencentOS Server 3.1
 - CentOS 7.6 or above
 - Ubuntu 18.10 or above
</dx-alert>

## Prerequisites
You have created and logged in to an [M6p instance](https://intl.cloud.tencent.com/document/product/213/11518).
- For detailed directions on how to create an instance, see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
- For detailed directions on how to log in to an instance, see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).


## Overview of Intel® Optane™ Persistent Memory (PMem) Modes

### Memory mode
In Memory mode, the regular DRAM serves as a cache for the most frequently accessed data, while the persistent memory is used as the backup memory. High-speed cache management operations are automatically processed by the memory controller.

### App Direct mode
The M6p model uses this mode. In an M6p instance, the BPS hardware configuration is set to App Direct mode and passed through to a CVM. In this mode, an application can use the PMem device as the memory or local SSD disk.


## Directions

### Initializing PMem
For the first time using the instance, run the following commands in sequence to initialize the PMem device. If you have initialized it, skip this step.
```
yum install -y ndctl
```
```
ndctl destroy-namespace all --force
```
<dx-alert infotype="explain" title="">
An instance with the highest specification has two regions. After running the following commands, replace `region0` with `region1` and run them again:
</dx-alert>
```
ndctl disable-region region0
```
```
ndctl init-labels all
```
```
ndctl enable-region region0
```

### Configuring PMem in App Direct mode

You can use the persistent memory as memory or local SSD disk based on your actual needs:

<dx-tabs>
::: Use as memory
PMem can be provided to upper-level applications (such as Redis) as a character device for assignment of persistent memory and can be used with a PMDK framework such as memkind. It is configured as follows:
1. Run the following command to generate a character device:
```
ndctl create-namespace -r region0 -m devdax
```
The returned result is as shown below, indicating that the `dax0.0` character device has been generated:
![](https://qcloudimg.tencent-cloud.cn/raw/e25e7a26c05b4d09507f571105d5e7c2.png)
An instance with the highest specification has two regions. If you use such an instance, you also need to run the following command:
```
ndctl create-namespace -r region1 -m devdax -f
```
After the configuration, the `dax0.0` character device is generated under the `/dev` directory, which can be mapped to the persistent memory.
2. Run the following command to view the persistent memory size:
```
ndctl list -R
```
The following information appears:
![](https://qcloudimg.tencent-cloud.cn/raw/b454a36bf3baf0361fe6154639b6c4da.png)


#### Extended feature (optional)
You can perform this step to use an extended feature. Run the following commands in sequence to use PMem to expand the CVM instance memory:
1. With the support of the kernel on a high version (above 5.1 and with KMEM DAX driver, such as kernel of TencentOS Server 3.1), you can configure PMem in devdax mode to KMEM DAX mode so as to use PMem to expand the CVM instance memory.
```
yum install -y daxctl
```
```
daxctl migrate-device-model
```
```
reboot
```
```
daxctl reconfigure-device --mode=system-ram --no-online dax0.0
```
The following information appears:
![](https://qcloudimg.tencent-cloud.cn/raw/6cc731b4e6e08be343c284683ac75721.png)
2. Run the following command to view the system memory expansion status:
```
numactl -H
```
The following information appears:
![](https://qcloudimg.tencent-cloud.cn/raw/6cbeee0aeb1bf7d4527297d5eaa747bc.png)
:::
::: Use as local SSD disk
PMem in App Direct mode can be configured as a general high-speed block device, where you can perform operations such as file system creation and raw disk read/write. It is configured as follows:
1. Run the following command to generate the `pmem0` block device under the `/dev` directory:
```
ndctl create-namespace -r region0 -m fsdax
```
The following information appears:
![](https://qcloudimg.tencent-cloud.cn/raw/010dbd1f35b3dfdff08d39546f0ce06e.png)
An instance with the highest specification has two regions. If you use such an instance, you also need to run the following command:
```
ndctl create-namespace -r region1 -m fsdax -f
```
2. Run the following command to create a file system or mount:
    1. Create a file system.
```
mkfs.ext4 /dev/pmem0
```
The returned result is as shown below, indicating that a file system is created successfully.
![](https://qcloudimg.tencent-cloud.cn/raw/e1c39d0122b4d6bff535d22dd9af0c18.png)
    2. Mount to `/mnt/`.
```
mount -o dax,noatime /dev/pmem0 /mnt/
```


:::
</dx-tabs>






## References
- [Intel® Optane™ DC Persistent Memory](https://www.intel.com/content/dam/support/us/en/documents/memory-and-storage/data-center-persistent-mem/Intel-Optane-DC-Persistent-Memory-Quick-Start-Guide.pdf)
- [Linux Provisioning for Intel® Optane™ Persistent Memory](https://www.intel.com/content/www/us/en/developer/articles/technical/qsg-part2-linux-provisioning-with-optane-pmem.html)

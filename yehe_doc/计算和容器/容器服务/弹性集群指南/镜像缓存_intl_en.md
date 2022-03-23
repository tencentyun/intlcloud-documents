

## Image Cache Overview

This document describes how image cache works and its billing rules, creation, and usage method. You can use image cache to accelerate image pull during instance creation so as to expedite instance startup. This capability is applicable to EKS cluster Pods, virtual nodes, and container instances.



## How It Works
When image cache accelerates instance startup, it will start a container instance in advance to pull the image, store the image in a data disk with a customizable size, and use the data disk as the cache of cloud disk snapshot, that is, the image data is already stored in the snapshot. You can choose to automatically or manually match the image cache when creating a container instance or Pod, and the specified number of data disks will be created based on the image snapshot and directly mounted to the instance to avoid image layer download, speeding up container instance and Pod creation.

Compared with the [image reuse](https://intl.cloud.tencent.com/document/product/457/43136) capability, image cache has the following strengths:
- It has no time limit and is only subject to the lifecycle of the image cache (snapshot).
- You only need to cold start a Pod in advance, which will be terminated immediately after snapshot creation.
- It has no limit on AZs, as AZs will be automatically matched during cloud disk creation based on snapshot.
- It has no limit on workloads, as workloads in the same region can be matched.


## Billing

The following resources are involved when you create an image cache, and their billing rules are as detailed below:


| Billable Item | Description | Document |
|---------|---------|---------|
| Image cache | When you create an image cache, you need to run a 2-core 4 GiB container instance to pull the image. After image cache creation, the container instance will be automatically released, and its billing will stop. | [Product Pricing](https://intl.cloud.tencent.com/document/product/457/34055) |
| CBS data disk | When you create an image cache, you need to bind a Premium Cloud Storage data disk to store the image. The disk size is customizable and 20 GB by default. After image cache creation, the data disk will be automatically released, and its billing will stop. | [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413) |
| Snapshot | A snapshot will be created based on the above-mentioned data disk, and its lifecycle will be the same as that of the image cache. It is billed by usage duration and capacity. | [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413#Snapshot) |

When the image cache is used, a Premium Cloud Storage data disk with the same capacity will be created based on the matched image cache snapshot and bound to the Pod. Therefore, in addition to the Pod creation fees, **data disk fees** will also be incurred.
- Data disk fees = capacity * unit price * instance running duration


## Directions

### Creating image cache
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2).
2. Select **EKS** > **Image Cache** on the left sidebar to enter the **Image Cache** page.
3. Click **Create Instance** and configure the relevant parameters.
  - Instance Name: optional.
  - Region: select as needed.
  - Container network: assign an IP address within the container network IP range to the container instance.
  - Security Group: a security group has the capabilities of a firewall and can limit the network communication of the instance. It is "default" by default.
  - Image: select the image and version to be cached as needed.
  - Image Credentials: when you select Docker Hub or a private image in a third-party image repository, you must enter the image credentials, i.e., access address, username, and password of the repository.
  - Advanced configuration:
     - Bind EIP: you need to bind an EIP to access the public network when pulling an image from the internet. 
     - Cache Size: it determines the size of the snapshot and the data disk bound during instance creation.
     - Expiration Policy: select the retention duration of the image cache, which is "Permanent" by default.
4. Click **Create**. After the image cache is created, it will be displayed in the image cache list. You can click the event name to view the creation progress.

### Using image cache
When creating an EKS Pod or container instance, you can enable image cache in **Advanced Configuration**. There are two image cache match methods, which you can select as needed.
<dx-tabs>
::: Automatic match
If you select **Automatic match**, the optimal image cache will be matched automatically according to the following match policy:

- If the image names and versions are completely the same, the image cache can be matched.
- Images with a smaller cache size will be matched first.
- Images with a later creation time will be matched first.

>! Note that if the versions are both "nginx:latest", the image cache can still be matched; however, as the creation time may be different, the versions may be inconsistent. Therefore, we recommend you specify the version clearly when creating an image cache and instance. 

If the corresponding image cache fails to be matched, an image will be pulled normally.
:::
::: Manual match
If you select **Manual match**, you need to manually select a specific image cache. Note that after you manually specify an image cache, a data disk will be directly created based on the image cache snapshot and bound to the instance. However, if the data disk does not have the image entered during instance creation (that is, an incorrect image cache is specified manually), an image will be pulled from the newly created data disk.

:::
</dx-tabs>

 

### Using image cache on virtual node

You can specify a Pod annotation to use an image cache on virtual nodes. For more information, see EKS [Annotation](https://intl.cloud.tencent.com/document/product/457/36162).

```
Automatically match:
eks.tke.cloud.tencent.com/use-image-cache: auto

Manually specify:
eks.tke.cloud.tencent.com/use-image-cache: imc-xxx
 
```



### Match result

You can check whether the match succeeds in the instance creation event.

If the image cache is matched successfully, the following event will be displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/06ed9dda35aa48af37c50e3c6985e1a2.png)
If this event is not displayed, no appropriate image caches have been matched.

Note that if you choose to manually match an image cache but it fails to be matched, an image will be pulled from the newly created data disk, and the following event will be displayed:
![](https://qcloudimg.tencent-cloud.cn/raw/8db338c2f36dc2dd39855a96fedc213d.png)


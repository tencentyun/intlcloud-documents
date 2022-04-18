## Overview
Tencent Cloud EMR comes with the ready-to-use Alluxio service, helping you accelerate distributed memory-level caching and simplify data management. You can also use the configuration delivery feature to configure multi-level caching and manage metadata via the EMR console or APIs. In addition, EMR offers one-stop monitoring and alarming.

## Preparations
- Tencent Cloud EMR Hadoop Standard v2.1.0 or above
- Tencent Cloud EMR Hadoop TianQiong v1.0 or above

For specific Alluxio versions supported in EMR, see [Component Version](https://intl.cloud.tencent.com/document/product/1026/31095).

## Creating an Alluxio-based EMR Cluster
This section describes how to create a ready-to-use Alluxio-based EMR cluster. You can create an EMR cluster via the purchase page or API.

### Creating a cluster via the purchase page
Go to the EMR [purchase page](https://buy.cloud.tencent.com/emr), choose an Alluxio-supported version, and select the Alluxio component in **Optional Components**.
![](https://main.qcloudimg.com/raw/c8c6a4ac0fdf5b4d4b952800284d6324.png)
Select other options as needed to meet your business needs. For reference, see [Creating EMR Cluster](https://intl.cloud.tencent.com/document/product/1026/31099).

### Creating a cluster via API
Tencent Cloud EMR also allows you to build a big data cluster based on Alluxio. For details, see [DescribeClusterNodes](https://intl.cloud.tencent.com/document/product/1026/35198).

## Basic Configurations
When you create an EMR cluster containing the Alluxio component, HDFS will be mounted to Alluxio and memory will be used for single-level (level 0) storage by default. You can use the configuration delivery feature to change the storage mode to multi-level storage or make other optimizations.
![](https://main.qcloudimg.com/raw/f7a77d3c53a6da12142deb92da3b710c.png)
After delivering configurations, you need to restart the Alluxio service for some configurations to take effect.
![](https://main.qcloudimg.com/raw/92a74cab2f3ccedd097193affe5e8a90.png)
For more details on configuration delivery and restarting policies, see [Configuration Management](https://intl.cloud.tencent.com/document/product/1026/31109) and [Restarting Services](https://intl.cloud.tencent.com/document/product/1026/31110).

### Storage and compute separation based on Alluxio acceleration
Tencent Cloud EMR provides the compute and storage separation capability based on Tencent Cloud COS. By default, when directly accessing the data in COS, applications do not have node-level data locality or cross-application caching. Alluxio acceleration helps alleviate these issues.

COS is deployed on Tencent Cloud EMR clusters by default and serves as the dependent JAR package of UFS. You only need to grant EMR clusters the permission to access COS and mount COS to Alluxio.

### Authorization
If COS is not enabled for the current cluster, you can go to **[CAM console > Roles](https://console.cloud.tencent.com/cam/role/grant?roleName=EMR_QCSRole&policyName=QcloudAccessForEMRRoleInApplicationDataAccess&principal=eyJzZXJ2aWNlIjoiZW1yLmNsb3VkLnRlbmNlbnQuY29tIn0=&serviceType=EMR&s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Femr%2Fstatic%2Fframework%2Femr-g9qk9p0g%3Ftype%3DinstanceDetail%26regionId%3D8)** to grant permission. After authorization, EMR nodes can access the data in COS using temporary keys.
![](https://main.qcloudimg.com/raw/6c5cc63c26123355119ed4e4302ef8a4.png)
![](https://main.qcloudimg.com/raw/41f988eba10c0e1b88a86cffe3c67e67.png)

### Mounting
Log in to any machine of EMR and mount COS to Alluxio.
```
bin/alluxio fs mount <alluxio-path> <source-path>
//TODO,
```
For more information on using Alluxio in Tencent Cloud EMR, see [Alluxio Development Documentation](https://intl.cloud.tencent.com/document/product/1026/31169).

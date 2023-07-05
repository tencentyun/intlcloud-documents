## Overview
This document describes how to create an ECM module in the console. An ECM module is the basic module for edge service management and composed of ECM instances. All instances in it use the same computing, network, and image configuration and provide the same service. By managing an ECM module, you can simplify scaling operations, which makes it easier for you to adjust the regional deployment of your business subsequently.

## Directions

1. Log in to the [ECM console](https://console.cloud.tencent.com/ecm/overview) and select **ECM Module** on the left sidebar.
2. On the ECM module page, click **Create Module**.
![](https://qcloudimg.tencent-cloud.cn/raw/f39fbfda6cebd5ce2f676eb9a10de66a.png)
3. On the module creation and instance configuration page, configure the following information as prompted:
![](https://qcloudimg.tencent-cloud.cn/raw/ede2b7f554722f08cc2701195551221d.png)
 - **Module Name**: it is the custom name of the ECM module to be created.
 - **Instance Type**: currently, **High I/O IT5** **Standard S4**, **High Private Network Bandwidth S4**, and **Standard SN3ne** models are supported. The performance of a model may vary slightly by scenario. For the specific performance differences, see [Instance Specification](https://intl.cloud.tencent.com/document/product/1119/43401).
 To make model selection during instance creation easier, we recommend you select **New Model First**. If this policy is enabled, the system will create an instance of the latest available model on your selected edge node. If there is no available latest model on the selected node, the system will create an instance in another available model.
 - **CPU Cores**: select a value as needed.
 - **Memory**: select a value as needed.
 - **Default Image**: Tencent Cloud provides public and custom images. We recommend new Tencent Cloud users select a pubic image.
 - **System Disk Storage**: it is 50 GB by default and cannot be adjusted.
 - **Data Disk Storage**: efficient and reliable storage devices are provided to expand the storage capacity of the ECM module. The default value is 0 GB, and the maximum value is 100 GB.
 - **Default Network Bandwidth Cap**: if the network bandwidth exceeds this cap, packets will be discarded by default. The default value is 25 Mbps, and the maximum value is 1,024 Mbps.
 - **Default Security Group**: a security group is a virtual firewall to control the network access of instances. You can go to the [Security Group](https://console.cloud.tencent.com/ecm/safe) page in the ECM console to create an ECM security group.
 - **Advanced Settings**: you can modify the settings of default IP direct access and default tags as needed:
     - **Default IP Direct Access**: the IP direct access feature is applicable for scenarios where the public IP needs to be viewed in edge CVM instances; for example, private network traffic and public network traffic need to be forwarded to different IP addresses.
     <dx-alert infotype="notice" title="">
     When you create a Linux ECM instance, the system will enable IP direct access by default (you can also disable it during instance creation in **Advanced Settings**). After an instance is created, the IP direct access status cannot be changed. If you create a Windows ECM instance, the system will not enable IP direct access by default (as Windows currently doesn't support IP direct access).
     </dx-alert>
    - **Default Tags**: you can set default tags to manage instances in the ECM module by group. During instance creation, the default tags set in the ECM module will be used as the recommended tag key-value pairs, and you can also modify them as needed.
     <dx-alert infotype="notice" title="">
      This configuration item only modifies the tag key-value pairs of the ECM module but doesn't automatically sync changes to those of successfully created instances.
      </dx-alert>
4. Click **OK**.
>? If the ECM module configuration provided in the console cannot meet your requirements, [submit a ticket](https://console.intl.cloud.tencent.com/workorder) for assistance, and a dedicated Tencent Cloud rep will contact you.

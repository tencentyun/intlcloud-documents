## Overview
This document describes how to create an ECM instance.

## Prerequisites
Before creating an ECM instance, you must complete the following operations:
- [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).
- [Create an ECM module](https://intl.cloud.tencent.com/document/product/1119/43421).
- If you want to use a Windows image, [submit a ticket](https://console.intl.cloud.tencent.com/workorder) for application or contact your Tencent Cloud rep.

## Directions

1. Log in to the [ECM console](https://console.cloud.tencent.com/ecm/overview) and select **Instance List** on the left sidebar.
2. On the instance list page, click **Add Instance** to enter the **Create and Deploy Instance** page.
3. Configure the following information as prompted by the page:
![](https://qcloudimg.tencent-cloud.cn/raw/46a23b1b3ca42a49e4a0415bb46d410e.png)
 - **Select Module**: select a module as needed.
 - **Default Image**: Tencent Cloud provides public and custom images. The image used by the module is selected by default. You can select an image as needed.
 - **Default Network Bandwidth Cap**: if the network bandwidth exceeds this cap, packets will be discarded by default. The default value is 25 Mbps, and the maximum value is 1,024 Mbps.
 - **Security Group**: a security group is a virtual firewall to control the network access of instances. The security group used by the module is selected by default. You can change the security group settings as needed.
 - **Advanced Settings**: you can modify the settings of default IP direct access and default tags as needed:
    - **IP Direct Access**: the IP direct access feature is applicable for scenarios where the public IP needs to be viewed in edge CVM instances; for example, private network traffic and public network traffic need to be forwarded to different IP addresses.
    <dx-alert infotype="notice" title="">
    When you create a Linux ECM instance, the system will enable IP direct access by default (you can also disable it during instance creation in **Advanced Settings**). After an instance is created, the IP direct access status cannot be changed. If you create a Windows ECM instance, the system will not enable IP direct access by default (as Windows currently doesn't support IP direct access).
    </dx-alert>
    - **Tags**: you can set default tags to manage instances in the ECM module by group. During instance creation, the default tags set in the ECM module will be used as the recommended tag key-value pairs, and you can also modify them as needed.
    <dx-alert infotype="notice" title="">
    This configuration item only modifies the tag key-value pairs of the ECM module but doesn't automatically sync changes to those of successfully created instances.
    </dx-alert>
 - **Instance Name**: it is the custom name of the instance to be created.
 - **Set Password** and **Confirm Password**: set the custom password for instance login.
7. Click **Next**.
8. On the **Region Deployment** tab of the **Create and Deploy Instance** page, configure the following information as prompted:
![](https://qcloudimg.tencent-cloud.cn/raw/3c834b87a5994c90107ff15aaa02c95a.png)
 - **Node Province**: we recommend you select the province closest to your end users to minimize the access latency and accelerate the access.
 - **Node Region**: select a region as needed.
 - **Network Type**: select a public network ISP as needed.
 - **Instance Quantity**: enter the number of ECM instances to be purchased.
 - **Activate CWP for Free**: it is selected by default to help you build a server security protection system to prevent data leakage.
 - **Activate CM for Free**: it is selected by default to activate CM free of charge. The CM agent will be installed to get the server monitoring metrics and display them as a monitoring icon, and you can customize the alarm thresholds.
9. Click **Confirm Purchase**.
After an instance is successfully created, its relevant information will be sent to you through the notification channel you subscribe to. You can also view the newly created resource in the [Instance List](https://console.cloud.tencent.com/ecm/instance).


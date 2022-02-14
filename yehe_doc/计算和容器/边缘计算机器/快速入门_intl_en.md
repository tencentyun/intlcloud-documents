
This document describes how to get started with ECM after you activate it under your Tencent Cloud account.

## Step 1. Register a Tencent Cloud account

If you already have a Tencent Cloud account, you can ignore this step.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;">Click here to register a Tencent Cloud account</a></div>

## Step 2. Apply for service activation

<div style="background-color:#00A4FF; width: 350px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/ecm" target="_blank"  style="color: white; font-size:16px;">Click here to log in to the ECM console</a></div>
</br>

![](https://main.qcloudimg.com/raw/6bd1b4beb9ad04eae864541732ca53f9.png)
On the **Activate Service** page in the ECM console, click **Submit Application** to enter the application page, enter the user information, submit the application, and wait for approval.
After your application is approved, you can create and use ECM resources.

## Step 3. Create an ECM module
1. Log in to the [ECM console](https://console.cloud.tencent.com/ecm/overview) and select **ECM Module** on the left sidebar.
2. On the ECM module page, click **Create Module**.
![](https://main.qcloudimg.com/raw/0f31271f9fcde99a4335c9b8fc255229.png)
3. On the module creation and instance configuration page, configure the following information as prompted:
![](https://main.qcloudimg.com/raw/6e6bc4b396fb3a0b148c301de872ea41.png)
 - **Module Name**: it is the custom name of the ECM module to be created.
 - **Instance Type**: currently, **High I/O IT5** **Standard S4**, **High Private Network Bandwidth S4**, and **Standard SN3ne** models are supported. The performance of a model may vary slightly by scenario. For the specific performance differences, see [Instance Specification](https://intl.cloud.tencent.com/document/product/1119/43401).
 - **CPU Cores**: select a value as needed. The default value is 8 cores.
 - **Memory**: select a value as needed. The default value is 16 GB.
 - **Default Image**: Tencent Cloud provides public and custom images. We recommend new Tencent Cloud users select a pubic image.
 - **System Disk Storage**: it is 50 GB by default and cannot be adjusted.
 - **Data Disk Storage**: efficient and reliable storage devices are provided to expand the storage capacity of the ECM module. The default value is 0 GB, and the maximum value is 100 GB. To increase the upper limit, [submit a ticket](https://console.intl.cloud.tencent.com/workorder) or contact your Tencent Cloud rep.
 - **Default Network Bandwidth Cap**: if the network bandwidth exceeds this cap, packets will be discarded by default. The default value is 25 Mbps, and the maximum value is 1,024 Mbps. To increase the upper limit, [submit a ticket](https://console.intl.cloud.tencent.com/workorder) or contact your Tencent Cloud rep.
 - **Advanced Settings**: you can modify the settings of default IP direct access and default tags as needed:
    - **Default IP Direct Access**: the IP direct access feature is applicable for scenarios where the public IP needs to be viewed in edge CVM instances; for example, private network traffic and public network traffic need to be forwarded to different IP addresses.
    <dx-alert infotype="notice" title="">
    When you create a Linux ECM instance, the system will enable IP direct access by default (you can also disable it during instance creation in **Advanced Settings**). After an instance is created, the IP direct access status cannot be changed. If you create a Windows ECM instance, the system will not enable IP direct access by default (as Windows currently doesn't support IP direct access).
    </dx-alert>
    - **Default Tags**: you can set default tags to manage instances in the ECM module by group. During instance creation, the default tags set in the ECM module will be used as the recommended tag key-value pairs, and you can also modify them as needed.
    <dx-alert infotype="notice" title="">
    This configuration item only modifies the tag key-value pairs of the ECM module but doesn't automatically sync changes to those of successfully created instances.
    </dx-alert>
4. Click **OK** to enter the details page of this ECM module.

## Step 4. Create an instance

1. Click **Create ECM Instance** as shown below:
![](https://main.qcloudimg.com/raw/52445f2cbc074aee131ebfdde4181c63.png)
2. On the **Password, Image, and Bandwidth** tab of the **Create and Deploy Instance** page, configure the following information as prompted:
	![](https://main.qcloudimg.com/raw/38ca39004bd78ae3bac729bfa2d2d383.png)
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
3. Click **Next**.
4. On the **Region Deployment** tab of the **Create and Deploy Instance** page, configure the following information as prompted:
![](https://main.qcloudimg.com/raw/5daf2418a19cbd6a202a183975c56a5d.png)
 - **Node Province**: we recommend you select the province closest to your end users to minimize the access latency and accelerate the access.
 - **Node Region**: select a region as needed.
 - **Network Type**: select a public network ISP as needed.
 - **Instance Quantity**: enter the number of ECM instances to be purchased.
5. Click **Confirm Purchase**.
After an instance is successfully created, its relevant information will be sent to you through the notification channel you subscribe to. You can also view the newly created resource in the [Instance List](https://console.cloud.tencent.com/ecm/instance).
<dx-alert infotype="notice" title="">
ECM has two billable items: computing storage and network bandwidth. Computing storage is billed by daily peak resource usage; that is, resources you add before midnight every day will be included in the calculation of the daily peak resource usage and may increase the total daily fees. Therefore, you should pay attention to the time point when you create a resource and avoid creating resources too late on a day, as that may increase the daily fees. For more information on billing, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1119/43404).
</dx-alert>


## Step 5. Log in to the instance

After creating an ECM instance, you can log in to it as instructed in [Logging in to Linux Instance](https://intl.cloud.tencent.com/document/product/1119/43412).

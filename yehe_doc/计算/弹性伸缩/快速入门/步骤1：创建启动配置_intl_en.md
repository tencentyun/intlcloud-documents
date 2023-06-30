## Overview
A launch configuration defines the configuration information of CVM instances used for auto scaling, including their images, storage, networks, security groups, login methods, and other configuration information.

<dx-alert infotype="explain" title="">
Creating a launch configuration is **free of charge**.
</dx-alert>

 


## Directions
### Selecting a region
1. Log in to the Auto Scaling console and click **[Launch Configuration](https://console.cloud.tencent.com/autoscaling/config)** in the left sidebar.
2. At the top of the **Launch configuration** page, select the project and region of the launch configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/0b5bc7d29a2c1a846b5d7eacabadb7f7.png)
CVM instances and CLB instances must be in the same region as the one specified for launch configuration. For example, if the Guangzhou region is specified for the launch configuration, only CVM instances in Guangzhou will be automatically added to the scaling group. For a scaling group in Guangzhou, you cannot add CVM instances or bind CLB instances from other regions (such as Shanghai, Beijing, Hong Kong (China), or Toronto).
3. Click **Create** to go to the **Create a launch configuration** page.



### Selecting a model
Set up the launch configuration name, availability zone, and model.
![](https://qcloudimg.tencent-cloud.cn/raw/91fed0ecdc2adcb399b0a51088cae846.png)

- **Launch configuration name**: Set the name of the launch configuration.
- **Billing mode**: Support **[Pay As You Go](https://intl.cloud.tencent.com/document/product/213/2180)** and **[Spot Instance](https://intl.cloud.tencent.com/document/product/213/17816)**.
- **Availability zone, model**: Select the model of the instance to be bound with the scaling group.


### Selecting images, storage, and bandwidth
1. When creating a launch configuration, you can use a public image, custom image or shared image. For more information, see [Image Overview](https://intl.cloud.tencent.com/document/product/213/4940).
![](https://qcloudimg.tencent-cloud.cn/raw/24c10101a7fb253f41796287a18ee193.png)
We recommend that you use a custom image where the application environment has already been deployed for the following reasons:
	- If you select a **public image**, the CVM instances created in a scaling group will have an operating system without the application environment. Then, you need to manually deploy the application environment.
	- If you select a **custom image**, you can use the image created for a CVM instance with an environment that has been deployed to batch create CVM instances have the same software environment as the original CVM, so as to implement batch deployment.
<dx-alert infotype="explain" title="">
For more information about creating images for CVM instance to be bound to a scaling group, see [Creating a Custom Image](https://intl.cloud.tencent.com/document/product/213/4942).
</dx-alert>
2. Set the disks in the launch configuration.
	![](https://qcloudimg.tencent-cloud.cn/raw/7a6a1f32ae55245058c65999a698d56e.png)
	If you specify a cloud disk as the system disk, you can create a data disk using data disk snapshots:
	- Users with a large amount of data often use data disks to store data. You can create a snapshot for data disk A, and use this snapshot to quickly clone multiple disks for rapid server deployment.
	- When a new CVM instance is automatically added for Auto Scaling, if you've specified a snapshot for the data disk in the launch configuration, CBS automatically mounts a data disk to the launched CVM instance to copy data.
	- If a data disk snapshot is specified in the launch configuration, ensure that the data disk can be automatically mounted correctly so that the scaling group can be scaled out automatically. The snapshot of the data disk of the original instance should be taken before auto scaling is configured so that data disks can be automatically mounted when new CVM instances are activated. For more information, see [Attaching Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).
3. An independent public IP address is allocated by default at no charge. Please select a network billing method based on your actual needs.
![](https://qcloudimg.tencent-cloud.cn/raw/3778935c55389ae9cb20ad42a6d2547b.png)
<dx-alert infotype="explain" title="">
 Auto Scaling is free of charge, but the added CVM instances, disks, and networks are billed in pay-as-you-go mode. Prices will be shown based on your configurations.
</dx-alert>


### Setting information
1. In the "Configure the CVM" step, select the login method and security group. By default, CVM instances created by Auto Scaling are protected by Cloud Security and Cloud Monitor free of charge.
![](https://qcloudimg.tencent-cloud.cn/raw/b145aee742dab16cac87119d5d3258d6.png)
2. After configuration confirmation and successful creation, you can view created launch configurations on the **Launch Configuration** page.
![](https://qcloudimg.tencent-cloud.cn/raw/e3dfde86a16e07aa0149c05bb7b22a20.png)

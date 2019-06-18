A launch configuration defines the information that is required for a scaling group to launch CVM (Cloud Virtual Machine) instances. The information includes CVM's image, storage, network, security group, and login method.  
>? Creating a launch configuration is **free of charge**.

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Launch Configuration** to go to the launch configuration management page.

## Selecting a Region

1. Specify the region of CVM that you would like to bind to the scaling group.
CVM instances and CLB instances must be the same region as the one specified for launch configuration. For example, when Guangzhou is specified for the launch configuration, only CVM instances in Guangzhou will be automatically added in the scaling group.  In a scaling group in Guangzhou, you cannot add CVM instances or bind CLB instances in any region (e.g., Shanghai, Beijing, Hong Kong, Toronto) other than Guangzhou.  
![Select a region](https://main.qcloudimg.com/raw/07a746c4f69b1a8641b74ce1ddc5cf4f.png)

## Selecting a Model

1. Click ![](//mccdn.qcloud.com/static/img/9d38f7bfbe02a922370765f3adfa58bf/image.png) to pop up the **Create a launch configuration** page.
2. On the **Create a launch configuration** page, enter the launch configuration name, select the availability zone, and select the model. See the figure below:
![](https://main.qcloudimg.com/raw/a38b03bb3c23c1393169598fcb195897.png)
 - Launch configuration name: Enter a name for your launch configuration.
 - Instance: Select the same model as the CVM instance that you want to bind to the scaling group.
3. Click **Next: Select an Image**.

## Selecting an Image

1. On the "2. Select an image" page, set the image type, OS, system architecture, and image version. See the figure below:
![Select an image](https://main.qcloudimg.com/raw/9459776ded2df48d711cf4b6a2bb77a4.png)
 - Image: When creating a launch configuration, you can use either public or custom image. However, custom images are recommended.
    - Public images must have the same operating system as the CVM instance that you want to bind to the scaling group.
    - Custom images must be created via CVM’s Create Custom Image feature. 
 - Operating System(OS): You can select CentOS, CoreOS, Debian, SUSE or Windows.
 - System architecture: You can select 64-bit or 32-bit.
 - Image version: You can select an image version.
 
 >?  
 > - Differences between public image and custom image: If you select a public image, the  CVM instances created in a scaling group will have a "clean" operating system - you need to manually deploy the application environment. Custom images enables batch production. You can create an image of a CVM instance with application environment deployed, and then use the image to batch create many CVM instances which will have the same application environment as the original instance. This enables you to deploy the same software environment in multiple instances.

 > - For more information about how to create an image for the CVM instance you would like bind to a scaling group, see [Creating a Custom Image](https://cloud.tencent.com/document/product/213/4942).
2. Click **Next: Select Storage and Bandwidth**.

## Selecting Storage and Bandwidth

1. On the "3. Select storage and bandwidth" page, set the disk and network. See the figure below:
![](https://main.qcloudimg.com/raw/c958b41819de424b6e4b7e414c92d71e.png)
>!  If you specify a CBS (Cloud Block Storage) disk as the system disk, you can create a data disk using data disk snapshots.

Disk data snapshot makes it easier to store Big data: snapshot a data disk, then use this snapshot to create more disks as needed. 

When a new CVM instance is added to Auto Scaling, if you've specified a snapshot for the data disk in launch configuration, CBS automatically mounts a data disk in the launched CVM instance to copy data.

In this case,  the data disk must be correctly mounted in the CVM instance to automatically scale out the scaling group. To auto-mount data dick in a new CVM instance, some additional operations on snapshot's original instance are required before setting up the automatic scaling. To learn about the operations, see [here](https://cloud.tencent.com/doc/product/362/5564).
>? AS is free of charge, but the added CVM instances, disks and networks are pay-as-you-go.
2. Click **4. Security Group and CVM**.

## Setting Information

1. On the "4. Security Group and CVM" tab, select the login method and security group. See the figure below:
>? By default, Auto Scaling-created CVM instances are protected by Cloud Security and Cloud Monitor for free, as shown below:
![](https://main.qcloudimg.com/raw/e7e5cba6e2c52b768e959a5db4c73bae.png)
2. Ensure all the information is correct and then click **Confirm**.
3. Click **Create a launch configuration**. After the configuration is completed, you will see this entry on the launch configuration list, as shown below: 
![](https://mc.qcloudimg.com/static/img/67ba31fd6c1f12485bb8f96220aaf6af/image.png)

A launch configuration defines the configuration information of CVM instances used for auto scaling, including their images, storage, networks, security groups, login methods, and other configuration information.
>? Creating launch configurations is free of charge.
>


## Selecting a Region

1. Log in to the Auto Scaling console and click **[Launch Configuration](https://console.cloud.tencent.com/autoscaling/config)** in the left sidebar.
2. At the top of the **Launch Configuration** management page, select the project and region of the CVM to be bound with the scaling group, as shown in the following figure:
![](https://main.qcloudimg.com/raw/014744e64c1b5bb3f251a478baa84540.png)
CVM instances and CLB instances must be in the same region as the one specified for launch configuration. For example, if the Guangzhou region is specified for the launch configuration, only CVM instances in Guangzhou will be automatically added to the scaling group. For a scaling group in Guangzhou, you cannot add CVM instances or bind CLB instances from other regions (such as Shanghai, Beijing, Hong Kong (China), or Toronto).


## Selecting the Model

1. Click **Create** to go to the **Create a launch configuration** page.
2. On the **Create a launch configuration** page, set the launch configuration name, availability zone, and model, as shown in the following figure:
![](https://main.qcloudimg.com/raw/0bd50d2d909e34deadd5d9681ba5f7e6.png)
 - **Launch configuration name**: enter a name for your launch configuration.
 - **Billing method**: only **pay-as-you-go** is supported. For more information, see [Pay as You Go](https://intl.cloud.tencent.com/document/product/213/2180).
 - **Availability zone and instance**: select the model of the instance to be bound with the scaling group.

## Selecting an Image
Set the image type, operating system, system architecture, image version, and other information, as shown in the following figure:
![](https://main.qcloudimg.com/raw/51d1974f89849862c8a4536f02864c2a.png)
 - **Image**: you can select a public image, custom image, or shared image. For more information, see [Image Overview](https://intl.cloud.tencent.com/document/product/213/4940). We recommend using custom images.
    - If you select a public image, it should be consistent with the operating system of the CVM to be bound with the scaling group.
    - If you select a custom image, you must create the image yourself using the CVM image creation feature.
 - **Operating System (OS)**: you can select CentOS, CoreOS, Debian, SUSE, or Windows.
 - **System architecture**: you can select 64-bit or 32-bit.
 - **Image version**: you can select an image version.
 >?  
 > - Differences between public images and custom images: if you select a public image, the CVM instances created in the scaling group are not automatically activated and cannot be used directly. You need to manually deploy the application environment. If you select **Custom Image**, you can use the image created for a CVM instance with an environment that has been deployed to batch create CVM instances have the same software environment as the original CVM, so as to implement batch deployment.
 > - For more information on creating CVM instances to be bound to a scaling group, see [Creating a Custom Image](https://intl.cloud.tencent.com/document/product/213/4942).


## Selecting Storage and Bandwidth

1. Set the disks and network, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2ef5c1920b6e1fbb46a9a17c5de91529.png)
If you specify a cloud disk as the system disk, you can create a data disk using data disk snapshots:
 - Users with a large amount of data often use data disks to store data. When a data disk creates a snapshot file, you can use the snapshot file to quickly clone multiple disks for rapid CVM deployment.
 - When a new CVM instance is automatically added for Auto Scaling, if you've specified a snapshot for the data disk in the launch configuration, CBS automatically mounts a data disk to the new CVM instance to copy data.
 - If a data disk snapshot is specified in the launch configuration, ensure that the data disk can be automatically mounted correctly so that the scaling group can be scaled out automatically. The snapshot of the data disk of the original instance should be taken before auto scaling is configured so that data disks can be automatically mounted when new CVM instances are activated. For more information, see [Auto Mounting](https://intl.cloud.tencent.com/document/product/362/32401).
>? Auto Scaling is free of charge, but the added CVM instances, disks, and networks are billed in pay-as-you-go mode. Prices will be shown based on your configurations.
2. Click **Next: complete Configuration**.

## Setting Information

1. In the **Complete Configuration** step, select the login method and security group, as shown in the following figure:
![](https://main.qcloudimg.com/raw/26b2f98e3a32eb5d9a50af56fbe6eb1e.png)
>? By default, Auto Scaling-created CVM instances are protected by Cloud Security and Cloud Monitor for free.
2. Click **Next: confirm Configuration** to check and confirm the configuration information.
3. Click **Create Launch Configuration**. After completing creation, you can view the created launch configuration on the **Launch Configuration** page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/7b25c445cf77fecdcf9c67b1f5431a70.png)

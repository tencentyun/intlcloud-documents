A launch configuration defines the configuration information of CVM instances used for auto scaling, including their images, storage, networks, security groups, login methods, and other configuration information.
>? Creating launch configurations is free of charge.
>


## Selecting a Region

1. Log in to the Auto Scaling console and click **[Launch Configuration](https://console.cloud.tencent.com/autoscaling/config)** in the left sidebar.
2. At the top of the **Launch Configuration** management page, select the project and region of the CVM to be bound with the scaling group, as shown in the following figure:
![](https://main.qcloudimg.com/raw/4cf018cd419dd5c86cfc3044142146a0.png)
CVM instances and CLB instances must be in the same region as the one specified for launch configuration. For example, if you select the Guangzhou region for the launch configuration, the scaling group can add CVM instances and bind CLB instances only in Guangzhou.


## Selecting the Model

1. Click **Create** to go to the **Create Launch Configuration** page.
2. On the **Create Launch Configuration** page, set the launch configuration name, availability zone, and model, as instructed below:
![](https://main.qcloudimg.com/raw/d98228bf350a7e5c431379f551804728.png)
 - **Launch configuration name**: enter a name for your launch configuration.
 - **Billing Mode**: select either **Pay as you go** or **Spot Instances**. For more information, see [Instance Billing Modes](https://intl.cloud.tencent.com/document/product/213/2180).
 - **Availability zone and instance**: select the model of the instance to be bound with the scaling group.

## Selecting an Image
Set the image type, operating system, system architecture, image version, and other information, as shown in the following figure:
![](https://main.qcloudimg.com/raw/68fdf834fc8c9e80a01b0ec466ec69ba.png)

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

1. Set the disks and network, as instructed below:
![](https://main.qcloudimg.com/raw/815cd3616ddccd7b6f8ad507d6b7575f.png)
If you specify a cloud disk as the system disk, you can create a data disk using data disk snapshots:
 - Users with a large amount of data often use data disks to store data. You can create a snapshot for the data disk, and use this snapshot to quickly clone multiple disks for rapid CVM deployment.
 - When a new CVM instance is automatically added for Auto Scaling, if you've specified a snapshot for the data disk in the launch configuration, CBS automatically mounts a data disk to the new CVM instance to copy data.
 - If a data disk snapshot is specified in the launch configuration, ensure that the data disk can be automatically mounted correctly so that the scaling group can be scaled out automatically. The snapshot of the data disk of the original instance should be taken before auto scaling is configured so that data disks can be automatically mounted when new CVM instances are started. For more information, see the “Automatic Mounting” section in [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).
>? Auto Scaling is free of charge, but the added CVM instances, disks, and networks are billed in pay-as-you-go mode. Prices will be shown based on your configurations.
2. Click **Next: Complete Configuration**.

## Setting Information

1. On the **Complete Configuration** page, select the login method and security group, as shown in the following figure:
![](https://main.qcloudimg.com/raw/dde466f2afe36030fcd36e7da6eb474b.png)
>? By default, CVM instances created by Auto Scaling are protected by Cloud Security and Cloud Monitor for free.
2. Click **Next: Confirm Configuration** to check and confirm the configuration information.
3. Click **Create Launch Configuration**. After completing creation, you can view the created launch configuration on the **Launch Configuration** page, as shown in the following figure:
![](https://main.qcloudimg.com/raw/7b25c445cf77fecdcf9c67b1f5431a70.png)



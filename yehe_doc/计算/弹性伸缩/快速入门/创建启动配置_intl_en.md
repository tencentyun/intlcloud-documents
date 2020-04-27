A launch configuration defines the configuration information of CVM instances used for auto scaling, including the images, storage, networks, security groups, login methods, and other configuration information of the CVMs.
> Creating launch configurations is free of charge.
>
1. Log in to the [Auto Scaling console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Launch Configuration** to go to the launch configuration management page.

## Selecting a Region

1. Specify the region of the CVM that you want to bind to the scaling group, as explained below:
The selected region determines the scope of instances that can be manually added and CLBs that can be bound. For example, if the Guangzhou region is specified for the launch configuration, only CVM instances in Guangzhou will be automatically added to the scaling group. For a scaling group in Guangzhou, you cannot add CVM instances or bind CLB instances in any region (for example, Shanghai, Beijing, Hong Kong (China), and Toronto) other than Guangzhou.
![](https://main.qcloudimg.com/raw/014744e64c1b5bb3f251a478baa84540.png)

## Selecting a Model

1. Click **Create** to go to the "Create a launch configuration" page.
2. On the **Create a launch configuration** page, enter the launch configuration name, select the availability zone, and select the model, as shown in the following figure:
![](https://main.qcloudimg.com/raw/0bd50d2d909e34deadd5d9681ba5f7e6.png)
 - Launch configuration name: enter a custom name for your launch configuration.
 - Instance: select the same model as the CVM instance that you want to bind to the scaling group.
3. Click **Next: Select an Image**.

## Selecting an Image

1. On the "2. Select an image" page, set the image type, operating system, system architecture, and image tag, as shown in the following figure:
![Select an image](https://main.qcloudimg.com/raw/51d1974f89849862c8a4536f02864c2a.png)
 - Image: when creating a launch configuration, you can use public or custom images. However, custom images are recommended.
    - Public images must have the same operating system as the CVM instance that you want to bind to the scaling group.
    - Custom images must be created by using CVM’s Create Custom Image feature.
 - Operating System (OS): you can select CentOS, CoreOS, Debian, SUSE, or Windows.
 - System architecture: you can select 64-bit or 32-bit.
 - Image tag: you can select an image tag.
 
 >  
 > - Differences between a public image and a custom image: if you select a public image, the CVM instances created in a scaling group are not yet activated and cannot be used directly. Instead, you need to manually deploy the application environment. If you select a custom image, by creating an image for the CVM instance of which the environment has been deployed, and using the image as the operating system when batch creating CVM instances, the CVM instances will have the same software environment as the original CVM instance after successful creation. In this way, you can perform batch deploying software environments.
 > - For more information on how to create the image of a CVM to be bound to a scaling group, see [Creating a Custom Image](https://intl.cloud.tencent.com/document/product/213/4942).
2. Click **Next: Select Storage and Bandwidth**.

## Selecting a Storage and Bandwidth

1. On the "3. Select storage and bandwidth" page, set the disk and network, as shown in the following figure:
![](https://main.qcloudimg.com/raw/2ef5c1920b6e1fbb46a9a17c5de91529.png)
> If you specify a Cloud Block Storage (CBS) cloud disk as the system disk, you can create a data disk by using data disk snapshots.

 Users with a large amount of data often use data disks to store data. When a snapshot file is created for a data disk, users can use the file to quickly clone multiple disks, achieving rapid CVM deployment.

 When Auto Scaling automatically adds a new CVM instance, if a data disk snapshot is specified for the data disk in the launch configuration, Tencent Cloud cloud disks support the automatic mounting of the data disk containing the set data after the CVM instance is launched, meeting the needs of automatic data replication.

 If a data disk snapshot is specified in the launch configuration, you must ensure that the data disk can be automatically and corrently mounted so that the scaling group can be scaled out automatically. Before configuring auto scaling, you must perform some operations on the original instance of the data disk snapshot in order to support the automatic mounting of the data disk when a new CVM instance is launched. For more information on the directions, see [Mounting a Data Disk Automatically When Launching New Instances by Using Custom Images and Data Disk Snapshots](https://intl.cloud.tencent.com/document/product/362/32401).
> Auto Scaling is free of charge, but the added CVM instances, disks, and networks are billed on demand. Prices will be shown based on your configurations.
2. Click **4. Security Groups and CVMs**.

## Setting Information

1. On the "4. Security Groups and CVMs" page, select the login method and security group, as shown in the following figure:
![](https://main.qcloudimg.com/raw/26b2f98e3a32eb5d9a50af56fbe6eb1e.png)
> By default, Auto Scaling-created CVM instances are protected by Cloud Security and Cloud Monitor for free.
2. Click **5. Confirm Configuration Information** and check that all the configuration information is correct.
3. Click **Create a Launch Configuration**. After the configuration is completed, you will see a new entry in the launch configuration list, as shown in the following figure:
![](https://main.qcloudimg.com/raw/7b25c445cf77fecdcf9c67b1f5431a70.png)

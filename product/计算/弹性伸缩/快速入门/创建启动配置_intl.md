A launch configuration defines configuration information of the CVM instances for automatic scaling, including information of the CVM image, storage, network, security group, and login method.
>? Launch configurations can be created free of charge.

1. Log in to the [AS console](https://console.cloud.tencent.com/autoscaling/config).
2. In the left sidebar, click **Launch Configuration** to go to the launch configuration management page.

## Selecting a Region

1. Select the region of CVM that you would like to bind.
The choice of region limits the CVM instances that can be added and the CLB instances that can be bound. For example, if you select Guangzhou, then the CVM instances automatically added in the scaling group will only be instances in Guangzhou. In a scaling group in Guangzhou, you cannot add CVM instances or bind CLB instances of other regions such as Shanghai, Beijing, Hong Kong, or Toronto.
![Select a region](https://main.qcloudimg.com/raw/07a746c4f69b1a8641b74ce1ddc5cf4f.png)

## Selecting a Model

1. Click ![](//mccdn.qcloud.com/static/img/9d38f7bfbe02a922370765f3adfa58bf/image.png) to pop up the **Create a launch configuration** page.
2. On the **Create a launch configuration** page, enter the launch configuration name, select the availability zone, and select the model. See the figure below:
![](https://main.qcloudimg.com/raw/a38b03bb3c23c1393169598fcb195897.png)
 - Launch configuration name: Enter a custom launch configuration name.
 - Instance: Select the same model as the CVM instance that you want to bind to the scaling group.
3. Click **Next: Select an Image**.

## Selecting an Image

1. On the "2. Select an image" page, set the image type, OS, system architecture, and image version. See the figure below:
![Select an image](https://main.qcloudimg.com/raw/9459776ded2df48d711cf4b6a2bb77a4.png)
 - Image: The images are divided into public images and custom images. It is recommended to select a custom image.
    - If a public image is selected, it must have the same OS as the CVM instance that you want to bind to the scaling group.
    - If a custom image is selected, it should be created by using the image creation feature of CVM.
 - OS: You can select an OS such as CentOS, CoreOS, Debian, SUSE, or Windows.
 - System architecture: You can select 64-bit or 32-bit.
 - Image version: You can select an image version.
 
 >?  
 > - Differences between public image and custom image: If you select a public image, the CVM instances produced during scale-out are not activated and cannot be used directly, and you have to manually deploy the application environment. If you select a custom image, by creating an image of a CVM instance where the environment has already been deployed, you can use that image as the OS when batch creating CVM instances. The instances created will have the same software environment as the original instance. This enables you to deploy the same software environment in multiple instances.
 > - For more information about how to create an image for the CVM instance you would like bind to a scaling group, see [Creating a Custom Image](https://cloud.tencent.com/document/product/213/4942).
2. Click **Next: Select Storage and Bandwidth**.

## Selecting Storage and Bandwidth

1. On the "3. Select storage and bandwidth" page, set the disk and network. See the figure below:
![](https://main.qcloudimg.com/raw/c958b41819de424b6e4b7e414c92d71e.png)
>! If you select a CBS cloud disk as the system disk, then you can select a data disk snapshot for the data disk.

 If you have large amounts of data, you need lots of data disks to store data. By creating a snapshot file of a data disk, you can use the snapshot file to quickly clone multiple disks for rapid deployment of servers.

 When AS automatically adds a new CVM instance, if the data disk snapshot is specified as the data disk in the launch configuration, CBS can automatically mount a data disk containing the set data to the CVM instance when it is launched, so as to implement automatic data copying.

 If the data disk snapshot is specified in the launch configuration, it must be ensured that the data disk can be automatically mounted correctly, so that the scaling group can be automatically scaled out. In order to allow automatic data disk mounting when new CVM instances are launched, you need to perform certain operations on the original instance based on which to create the data disk snapshot before setting automatic scaling. For more information, see [here](https://cloud.tencent.com/doc/product/362/5564).
>? AS is free of charge, but the added CVM instances, disks and networks are pay-as-you-go.
2. Click **4. Security Group and CVM**.

## Setting Information

1. On the "4. Security Group and CVM" tab, select the login method and security group. See the figure below:
![](https://main.qcloudimg.com/raw/e7e5cba6e2c52b768e959a5db4c73bae.png)
> The CVM instances produced by AS enjoy Cloud Security and Cloud Monitor services for free by default.
2. Click **5. Confirm** to check and confirm the configuration information.
3. Click **Create a launch configuration**. After the configuration is completed, this entry will be displayed in the launch configuration list on the page, as shown below:
![](https://mc.qcloudimg.com/static/img/67ba31fd6c1f12485bb8f96220aaf6af/image.png)

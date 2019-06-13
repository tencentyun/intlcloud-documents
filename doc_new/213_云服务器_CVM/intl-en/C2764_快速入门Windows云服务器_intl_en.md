
This document describes how to easily use the features of CVM instances on Windows system and is designed to help beginners to get started with the creation and configuration of Tencent Cloud CVM quickly.

<div id="page1"></div>

## Step 1: Prepare and Select Model
### Sign up for a Tencent Cloud account
New users need to [register](https://intl.cloud.tencent.com/register) with Tencent Cloud official website. For more information, see [How to Sign up for Tencent Cloud](https://intl.cloud.tencent.com/document/product/213/6090).

### Specify the region and availability zone in which the CVM resides
How to select region:
 - Be close to your users.
The region of a CVM should be selected depending on your user's geographical location. The closer the CVM is to your users who access it, the shorter the access latency and the higher the access speed will be. For example, if most of your users are in North America, then Toronto is a good choice.
 - In the same region.
CVMs in the same region are interconnected with each other via a private network, but those in different regions cannot communicate with each other via a private network. Users who communicate with each other using multiple CVMs via a private network should choose the same region.
CVMs in the same region can communicate with each other via a private network free of charge.
CVMs in different regions cannot communicate with each other via a private network but only via a public network with a charge.

### Select CVM configuration solution
You can compare the configurations in [More Models](https://intl.cloud.tencent.com/document/product/213/11518) based on your actual needs. You can also [Upgrade Configuration](https://intl.cloud.tencent.com/document/product/213/2178#upgrading-configuration) or [Downgrade Configuration](https://intl.cloud.tencent.com/document/product/213/2178#degrading-configuration) at any time after purchasing a CVM based on your business needs.

### Choose a billing method
Tencent Cloud supports Postpaid billing method. For more information, see [Billing Methods](/doc/product/213/2180).
If Postpaid method is selected, you need to complete [Identity Verification](https://console.cloud.tencent.com/developer/infomation).

<div id="page2"></div>

## Step 2: Create a Windows CVM
This step describes how to create a Windows CVM.

 1. Log in to the Tencent Cloud official website, select **Products** -> **Cloud Compute & Network** -> **Cloud Virtual Machine**, then click **Experience** to enter the [CVM purchase page](https://console.cloud.tencent.com/cvm/index), and click **Create** to start the purchase.

 2. Select a region and model. Choosing a region close to your users can minimize access latency and improve download speed.

    ![image-20181009174217646](https://main.qcloudimg.com/raw/820aa02738c2d69b70090083e292eb4b.png)

 3. Select an image. Select a Windows operating system that meets your requirement.

    ![image-20181010105754025](https://main.qcloudimg.com/raw/ae628bc9aea84e55b0a691bb59de1b4a/image-20181010105754025.png)

 4. Select storage and public network bandwidth. If you do not need to connect to the public network, set the bandwidth value to 0.

    ![image-20181009174426285](https://main.qcloudimg.com/raw/5cfedc485adae3943823ed7920f26aad.png)

 5. Set the security group, account name and login method.

    ![image-20181009174512418](https://main.qcloudimg.com/raw/08f3348cb809b812cd9bde269e21ce41.png)

 6. Confirm the settings of the CVM and select quantity.

    ![image-20181009174613350](https://main.qcloudimg.com/raw/05578198df6ea198935c89b56546ecb8.png)

For more information on how to view internal messages, see the next step.

<div id="Inter-Page">  </div>

## Step 3: Log in to Windows CVM
This section describes how to log in to a Windows CVM. Login method varies depending on different scenarios. This step shows how to log in to the CVM through the console. For more information on other login methods, see [Log in to Windows Instance](/doc/product/213/5435).

### Prerequisites
You need to use the admin account ID and the corresponding password to log in to the CVM.

 * Admin account ID: It is always Administrator for Windows instances
 * Password: For quick configuration, the initial password is randomly assigned by the system. For detailed operations, see the next section (View internal messages and CVM information).
   For more information, see [Login Password](/doc/product/213/6093).
### View internal messages and CVM information
After a CVM is purchased and created, the instance name, public IP, private IP, login name, initial login password, and other information of the CVM are sent to your account via [Internal Message](https://console.cloud.tencent.com/message).

 1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index), and you can see the public IP, private IP, and other information.

 2. Click **Internal Message** at the upper right corner.

 3. The new CVM and its information such as login name and password can be found in the Internal Message page, as shown in areas highlighted in yellow:

    ![image-20181009175141548](https://main.qcloudimg.com/raw/a52108b18b1ab2313a8b92661e3e4782.png)


### Log in to the CVM through the console
  1. Click the **Log In** button in the operation column on the CVM list page to select a proper login method:

    ![image-20181010111640723](https://main.qcloudimg.com/raw/04e1ff6540b7eeed3a9e27146c7f2f93/image-20181010111640723.png)

  2. To log in to your CVM via VNC, click **Log In Now**.

  ![image-20181010111900601](https://main.qcloudimg.com/raw/9866809b13da4987f8396e75edce253d/image-20181010111900601.png)

 3. Select **Ctrl-Alt-Delete** from the top left corner, and go to the system login page:
    ![](https://main.qcloudimg.com/raw/9cc783ce08888c817f48a5286d87fa86/WeChatWorkScreenshot_4a450c90-11b4-4490-bc08-5d95d1f95bfe.png)

 4. Enter the account ID (Admin) and the initial password from the internal message (or the password modified by you) to log in.

>**Note:**
>This terminal is exclusive, that is, only one user can log in using the console at a time.

<div id="page4"></div>

## Step 4: Partition and Format Data Disk

Here, we use Windows Server 2012 R2 DataCenter 64bit EN to explain how to format a data disk.

### Prerequisites

 - Users who have purchased a data disk need to format it before use, and those who have not purchased a data disk can skip this step.
 - Make sure you have completed Step 3 to log in to the CVM.

### Format the data disk

1. Log in to your Windows CVM by following the method described in Step 3.

2. Click **Start** -> **Server Manager** -> **Tools** -> **Computer Management** -> **Storage** -> **Disk Management**.

   ![image-20181010120646197](https://main.qcloudimg.com/raw/f988db357f1daae7b6d2c35a7d20bc68/image-20181010120646197.png)

   ![image-20181010120817988](https://main.qcloudimg.com/raw/5cf806c9fff23e19fbede4a7334c4e37/image-20181010120817988.png)

   ![image-20181010121020945](https://main.qcloudimg.com/raw/4e43326adbcb539af918ef40302b24da/image-20181010121020945.png)

3. Right click on Disk 1 and select **Online**. If this disk is already online, you can skip this step.

   ![image-20181010143149191](https://main.qcloudimg.com/raw/5df2d05297fb9cf617f426369ecd0421/image-20181010143149191.png)

4. Right click and select **Initialize Disk**:

  ![image-20181010143401964](https://main.qcloudimg.com/raw/63ec811fecb252eecc569ade10944c1e/image-20181010143401964.png)




Select **GPT** or **MBR** depending on the partitioning method, and click the **OK** button:

> Note:
> Make sure to select GPT as partitioning method if the disk is larger than 2 TB. If you are not sure whether the disk capacity will exceed this value after subsequent expansion, GPT partitioning format is recommended. If you're sure that the disk capacity will not exceed this value, you're recommended to select MBR partitioning for a better compatibility.*

 ![image-20181010143526150](https://main.qcloudimg.com/raw/30d5a469940766d7aa36f6abad63f71c/image-20181010143401964.png)

## Disk Partitioning (Optional)

1. Right click on the unallocated space, and select **New Simple Volume**:

   ![image-20181010143857453](https://main.qcloudimg.com/raw/d2facf7e459d89501a18bfe339415666/image-20181010143857453.png)

2. In the **New Simple Volume Wizard** pop-up window, click **Next**:

   ![image-20181010144003766](https://main.qcloudimg.com/raw/21aef4b0d7d4a54b960fd564216fefbe/image-20181010144003766.png)

3. Enter the desired disk size for the partition, and click **Next**:

   ![image-20181010144105132](https://main.qcloudimg.com/raw/b7f9354ff8a28543dbe3777af8f595c0/image-20181010144105132.png)

4. Enter the drive letter, and click **Next**:

   ![image-20181010144206060](Getting started with CVM on Windows_intl_cn.assets/image-20181010144206060.png)

5. Select **File System** -> **Format Partition**, and click **Next**:

   ![image-20181010144307006](https://main.qcloudimg.com/raw/e4d65c61310e9515742143e3648605e5/image-20181010144206060.png)

6. Upon completing the New Simple Volume operation, click **Finish**:

   ![image-20181010144335711](https://main.qcloudimg.com/raw/04716f7b2dd855513d8767236f43aa37/image-20181010144335711.png)

7. Open **This PC** in **Start** to view the new partition.

   ![image-20181010144445290](https://main.qcloudimg.com/raw/ded8b50737ffe1d6d342bf604d9a9474/image-20181010144445290.png)

**Now, you have completed the creation and basic configuration of a Windows CVM.**


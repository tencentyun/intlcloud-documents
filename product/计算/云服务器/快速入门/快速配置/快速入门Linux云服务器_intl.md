
This document describes how to create and configure a Linux-based CVM instance.

<div id="page1"></div>

## Step 1: Prepare and Select Model
### Sign up for a Tencent Cloud account
For users new to Tencent Cloud, please [register](https://intl.cloud.tencent.com/register) on Tencent Cloud official website first. For more information, see [How to Sign up for Tencent Cloud](https://intl.cloud.tencent.com/document/product/213/6090).

### Specify the region and availability zone
How to select region:
 - Be close to your users
Choose the region closest to your end users, so as to reduce the network latency and increase the access speed. For example, if most of your users are in North America, then Toronto is a good choice.
 - In the same region
CVMs in the same region are interconnected with each other via a private network, but those in different regions cannot communicate with each other via a private network. Users who communicate with each other using multiple CVMs via a private network should choose the same region.
CVMs in the same region can communicate with each other via a private network free of charge.
CVMs in different regions cannot communicate with each other via a private network but only via Internet with a charge.

### Select CVM Model
You can compare the configurations in [More Models](https://intl.cloud.tencent.com/document/product/213/11518),and select models according to your actual needs. You can also [Upgrade Configuration](https://intl.cloud.tencent.com/document/product/213/2178#upgrading-configuration) or [Downgrade Configuration](https://intl.cloud.tencent.com/document/product/213/2178#degrading-configuration) later if required.

### Choose a billing method
Tencent Cloud supports pay-as-you-good billing method. For more information, see [Billing Methods](/doc/product/213/2180).

<div id="page2"></div>

## Step 2: Create a Linux-based CVM
Please follow the steps below to create a Linux-based CVM.

 1. Log in to the Tencent Cloud, select **Products** -> **Cloud Compute & Network** -> **Cloud Virtual Machine**, then click **Get Started** to enter the [CVM purchase page](https://console.cloud.tencent.com/cvm/index), and click **Create** to start the purchase.

 2. Select a region and model. Choosing a region close to your users can minimize network latency and improve download speed.

    ![image-20181009174217646](https://main.qcloudimg.com/raw/820aa02738c2d69b70090083e292eb4b.png)

 3. Select an image. Select a Linux operating system that meets your requirement.

    ![image-20181009174332701](https://main.qcloudimg.com/raw/672968dca61a9a48cd935c0f3d7f00cf.png)

 4. Complete storage configuration and set the internet bandwidth. If you do not need to connect to the internet, set the bandwidth value to 0.

    ![image-20181009174426285](https://main.qcloudimg.com/raw/5cfedc485adae3943823ed7920f26aad.png)

 5. Set the security group, account name and login method.

    ![image-20181009174512418](https://main.qcloudimg.com/raw/08f3348cb809b812cd9bde269e21ce41.png)

 6. Confirm the settings of the CVM and select quantity.

    ![image-20181009174613350](https://main.qcloudimg.com/raw/05578198df6ea198935c89b56546ecb8.png)

For more information on how to view internal messages, see the next step.

<div id="Inter-Page">  </div>

## Step 3: Log in to Linux CVM
This section describes how to log in to the CVM on the console. For more information on other login methods, see [Log in to Linux Instance](/doc/product/213/5436).

### Prerequisites
Log into the CVM with the admin account.

 * Admin account ID: "root" for Linux instances ("ubuntu" for Ubuntu system)
 * Password: If you choose "quick configuration", the initial password is randomly assigned by the system. You can check the password in internal message and email
   For more information, see [Login Password](/doc/product/213/6093).

### Checking CVM information
After a CVM is purchased and launched, we will send you information of this CVM (including the instance name, public IP, private IP, login name, initial login password) via [Tencent Cloud Internal Message](https://console.cloud.tencent.com/message).

 1. Log in to [CVM console](https://console.cloud.tencent.com/cvm/index), and you can see the public IP, private IP, and other information.

 2. Click **Internal Message** at the upper right corner.

 3. The new CVM and its information such as login name and password can be found in the Internal Message page, as shown in areas highlighted in yellow.

    ![image-20181009175141548](https://main.qcloudimg.com/raw/a52108b18b1ab2313a8b92661e3e4782.png)


### Log in to the CVM through the console
 1. Click the **Log In** button in the operation column on the CVM list page to log in to the Linux CVM:
    ![image-20181010110440283](https://main.qcloudimg.com/raw/501d857bac9c6bd38e8dc1761e105d28/image-20181010110440283.png)

 2. Enter the account ID "root" (or the username you set) and the initial password from the internal message (or the modified password) to log in.

    ![image-20181010110542743](https://main.qcloudimg.com/raw/1310dcb1b36927711d387b8180c2bfaa/image-20181010110542743.png)

<div id="page4"></div>

## Step 4: Partition and Format Data Disk

### Prerequisites
 - Users who have purchased a data disk need to format it before use, and those who have not purchased a data disk can skip this step.
 - Make sure you have completed Step 3 to log in to the CVM.
 - Mount data disks larger than 2 TB using GPT method. For more information, see [Partitioning and Formatting Data Disk with GPT Partition Table](https://intl.cloud.tencent.com/document/product/362/31602#formatting-new-space-as-an-independent-gpt-partition).

### Partition the data disk

 1. Log in to your Linux CVM by following the method described in Step 3.

	> **Note:**
	> It only supports partitioning the data disk, but not the system disk. Forced partitioning of the system disk may lead to system crash or other serious problems, for which Tencent Cloud shall not be held liable.

 2. Enter the command `fdisk -l` to check the data disk information.
	In this example, a 54 GB data disk `(/vdb)` needs to be mounted.
	>**Note:**
	> Both `fdisk -l` and `df -h` commands are used to check the data disk information. However, using the command `df -h` does not display the information of the data disk if it has not been partitioned and formatted.

	![](https://main.qcloudimg.com/raw/569122784140ce71fdb4e4ef6c936838.png)

 3. Partition the data disk. Perform the operations below by following the instructions on the page:

		(1) Enter `fdisk /dev/vdb` (partition the data disk), and press Enter.
	​	(2) Enter `n` (create a new partition), and press Enter.
	​	(3) Enter `p` (create an extended partition), and press Enter.
	​	(4) Enter `1` (use the first primary partition), and press Enter.
	​	(5) Press Enter (use default settings).
	​	(6) Press Enter again (use default settings).
	​	(7) Enter `wq` (save partition table), and press Enter to start partitioning.

	In this example, we only create one partition. Developers can create multiple partitions according to their own needs.
	![](https://main.qcloudimg.com/raw/719a604e35895630881dd3d2df60dbf5/image2.png)

 4. Use the command `fdisk -l` to check that the new partition vdb1 has been created.
	![](https://main.qcloudimg.com/raw/762c95fb196c1461fbfdfa15cb5ca908/image3.png)

### Format the data disk

 1. Format the new partition
 The new partition needs to be formatted. You can use a file system format based on your own needs, such as ext2 or ext3. In this example, ext3 is used.
Use the following command to format the new partition: 
	```
	mkfs.ext3 /dev/vdb1
	```
	![](https://main.qcloudimg.com/raw/8c1fcdbcb40dbb310e8d6c50b15bde70/image4.png)

 2. Mount the partition
	Use the following command to create a mydata directory and mount the partition under this directory:
	```
	mkdir /mydata
	mount /dev/vdb1 /mydata
	```
	Use the following command to view the status of mounting:
	```
	df -h
	```
	The information of vdb1 shown in the red box indicates that the mounting is successful and the data disk is displayed.
	![](https://main.qcloudimg.com/raw/9952f0aaaf35c124aa6c2a4df234e29a/image5.png)

 3. Configure auto mount upon startup
To allow your CVM to be automatically mounted with the data disk when it is restarted or started up, add the partition information to `/etc/fstab`.
Use the following command to add partition information:
	```
	echo '/dev/vdb1 /mydata ext3 defaults 0 0' >> /etc/fstab
	```
	Use the following command to make a check:
	```
	cat /etc/fstab
	```
	The information of vdb1 shown in the red box indicates that the partition information has been successfully added.
	![](https://main.qcloudimg.com/raw/8954037db435d0661330da00c38a9ee1/image6.png)
	

**Now, you have completed the creation and basic configuration of a Linux CVM.**


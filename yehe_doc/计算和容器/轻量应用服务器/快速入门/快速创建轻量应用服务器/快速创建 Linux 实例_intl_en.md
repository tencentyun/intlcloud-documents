This document describes how to purchase and start using a Lighthouse instance.

## Step 1. Sign up and top up
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/account/register).
If you already have a Tencent Cloud account, ignore this step.
2. [Top up online](https://console.cloud.tencent.com/expense/recharge).
Lighthouse instances are available through monthly subscription. To make a purchase, you need to top up your account as instructed in [Payment Methods](https://intl.cloud.tencent.com/document/product/555/7425).

## Step 2. Purchase a Linux Lighthouse instance

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Click **Create** to enter the Lighthouse purchase page.
![](https://qcloudimg.tencent-cloud.cn/raw/540a54ce93a72135d6e83e76917a767b.png)
 - **Region**: We recommend you select a region near your target users to reduce the network latency and improve their access speed.
 - **Availability zone**: **Randomly assigned** is selected by default. You can select one as well.
 - **Image**: Select your desired Lighthouse OS. The CentOS 8.0 system image is selected here as an example.
 - **Instance bundle**: Select an instance package according to the required instance configuration (including CPU, memory, system disk, bandwidth, and monthly traffic).
 - **Instance name**: Enter a custom instance name. If it is left empty, an "image name + 4-digit random string" will be used as the name by default. When multiple instances are created in a batch, their names will be consecutive with auto-incrementing suffixes. For example, if you enter "LH" as the name and purchase three instances, the three instances are named "LH1", "LH2", and "LH3".
 - **Purchase period**: Default to **1 month**.
 - **Quantity**: Default to **1**.
3. Click **Buy now**.
4. Confirm the configuration information is correct, click **Submit order** and make the payment as prompted.

After making the payment, the Lighthouse instance purchase will be successfully completed. Then, you can log in to the instance.

## Step 3. Log in to the Linux Lighthouse instance
Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), find the newly purchased instance in the instance list, and click **Log in**.
You will log in to the Linux instance through a webshell terminal without entering the password.
![](https://qcloudimg.tencent-cloud.cn/raw/2a6ea6b733d1c70af4d2f46777cfaa00.png)



## (Optional) Step 4. Reset the Linux Lighthouse instance password
If you want to use an SSH key or a remote login application to connect to the Linux instance, [reset the password](https://intl.cloud.tencent.com/document/product/1103/41553) or [set a key](https://intl.cloud.tencent.com/document/product/1103/41392) first. This step takes resetting the password as an example. Perform operations based on your actual needs.

1. In the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), find the newly purchased instance in the instance list and enter its details page.
2. On the instance details page, click **Reset password** in the top-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/d7771b962b2a7d568c53f38550978552.png)
3. In the **Reset password** pop-up window, enter and confirm the password as prompted. 
<dx-alert infotype="explain" title="">
- The password can be reset only when the instance is shut down. We recommend you shut down the instance first before resetting the password. If you want to reset the password when the instance is running, you should select **Agree to a forced shutdown**.
- If you use the Ubuntu image application to create an instance, the instance will disable login of the `root` user through password by default. If you need to enable it, see [How do I log in to an instance as the root user on Ubuntu?](https://intl.cloud.tencent.com/document/product/1103/41257).
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/d7517733ca0d5bc8f791a71cb0c85fcf.png"/>

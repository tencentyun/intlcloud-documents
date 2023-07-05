This document describes how to quickly purchase and use a Lighthouse instance.

## Step 1. Sign up and top up
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/account/register).
If you already have a Tencent Cloud account, ignore this step.
2. [Top up online](https://console.cloud.tencent.com/expense/recharge).
Lighthouse instances are available through monthly subscription. To make a purchase, you need to top up your account as instructed in [Payment Methods](https://intl.cloud.tencent.com/document/product/555/7425).

## Step 2. Purchase a Windows Lighthouse instance

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Click **Create** to enter the Lighthouse purchase page as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/540a54ce93a72135d6e83e76917a767b.png)
 - **Region**: We recommend you select a region near your target users to reduce the network latency and improve their access speed.
 - **Availability zone**: **Randomly assigned** is selected by default. You can select one as well.
 - **Image**: Select an OS as needed. The Windows Server 2022 system image is selected here as an example.
 - **Instance bundle**: Select an instance bundle according to the required instance configuration (including CPU, memory, system disk, bandwidth, and data transfer plan).
 - **Instance name**: Enter a custom instance name. If it is left empty, an "image name + 4-digit random string" will be used as the name by default. When multiple instances are created in a batch, their names will be consecutive with auto-incrementing suffixes. For example, if you enter "LH" as the name and purchase three instances, the three instances are named "LH1", "LH2", and "LH3".
 - **Login method*: If you select a Windows image, you can use this option to set the login password of the instance:
    - **Set password**: Set the custom password for instance login.
    - **Random password**: The system sends an automatically generated password to your [Message Center](https://console.cloud.tencent.com/message).
 - **Purchase period**: Default to **1 month**.
 - **Quantity**: Default to **1**.
3. Click **Buy now**.
4. Confirm the configuration information is correct, click **Submit order** and make the payment as prompted.

## Step 3. Log in to the Windows Lighthouse instance

1. In the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), find the newly purchased instance in the instance list and click **Log in**.
You will log in to the Windows instance through a VNC terminal.
![](https://qcloudimg.tencent-cloud.cn/raw/681596d0b43ce610df25d090705d604b.png)
2. In the **Log in** pop-up window, select **Send remote command** in the top-left corner and press Ctrl+Alt+Delete to enter the system login page.
![](https://qcloudimg.tencent-cloud.cn/raw/c31cc671debcd51b8d51bf51c6201e3c.png)
3. Enter the login password and press **Enter** to log in to the instance.

In addition, you can use the local RDP tool (such as MSTSC that comes with Windows) to remotely connect to the Windows instance.

This document describes how to quickly purchase and use a Lighthouse instance.

## Step 1. Sign up
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/register) and complete identity verification. 
If you already have a Tencent Cloud account, you can ignore this step.

## Step 2. Purchase a Lighthouse Windows instance

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Click **Create** to enter the Lighthouse instance purchase page as shown below:

 - **Region**: we recommend you select a region near your target users to reduce the network latency and improve the access speed. For example, if your target users are in **Shenzhen**, you can select **Guangzhou** as the region.
 - **Image**: select your desired Lighthouse OS. The Windows Server 2012 R2 system image is selected here as an example.
 - **Instance Package**: select an instance package according to the required instance configuration (including CPU, memory, system disk, bandwidth or peak bandwidth, and monthly traffic).
 - **Instance Name**: enter a custom instance name. If it is left empty, "image name+four random characters" will be used as the name by default. When instances are created in batches, their names will be consecutive with auto-incrementing suffixes. For example, if you enter "LH" as the name and select 3 as the quantity, 3 instances "LH1", "LH2", and "LH3" will be created.
 - **Purchase Duration**: it is one month by default.
 - **Purchase Quantity**: it is one instance by default.
3. Click **Buy Now**.
4. After confirming that the configuration information is correct, click **Submit Order** and make the payment as prompted.

After making the payment, the Lighthouse instance purchase will be successfully completed. Then, you can log in to the instance.

## Step 3. Reset the Lighthouse Windows instance password
Before logging in to the Lighthouse Windows instance, you should set a password for the Lighthouse admin username (`Administrator`).
1. In the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), find the newly purchased instance in the server list and enter its details page.
2. In the **Instance Info** column, click **Reset Password**.

3. In the pop-up window, enter and confirm the password as prompted.
>? The password can be reset only when the instance is shut down. We recommend you shut down the instance first before resetting the password. If you want to reset the password when the instance is running, you should select **Agree to a forced shutdown**.
>


## Step 4. Log in to the Lighthouse Windows instance

1. In the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), find the newly purchased instance in the instance list and click **Log in**. 
You will log in to the Windows instance through a VNC terminal.

2. In the pop-up login window, select **Send Remote Command** in the top-right corner and press **Ctrl+Alt+Delete** to enter the system login page.

3. Enter the login password just reset and press **Enter** to log in to the instance.

In addition, you can use the local RDP tool (such as MSTSC that comes with Windows) to remotely connect to the Windows instance.

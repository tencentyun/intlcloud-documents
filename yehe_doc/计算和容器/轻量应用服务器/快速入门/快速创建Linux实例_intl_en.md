This document describes how to quickly purchase and use a Lighthouse instance.

## Step 1. Sign up
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/register) and complete identity verification. 
If you already have a Tencent Cloud account, you can ignore this step.

## Step 2. Purchase a Lighthouse Linux instance

1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Click **Create** to enter the Lighthouse instance purchase page.

 - **Region**: we recommend you select a region near your target users to reduce the network latency and improve the access speed. For example, if your target users are in **Shenzhen**, you can select **Guangzhou** as the region.
 - **Image**: select your desired Lighthouse OS. The CentOS 8.0 system image is selected here as an example.
 - **Instance Package**: select an instance package according to the required instance configuration (including CPU, memory, system disk, bandwidth or peak bandwidth, and monthly traffic).
 - **Instance Name**: enter a custom instance name. If it is left empty, a default name will be generated in the format of “[image name]-[4 random characters]". When instances are created in batches, their names will be consecutive with auto-incrementing suffixes. For example, if you enter "LH" as the name and select 3 as the quantity, 3 instances "LH1", "LH2", and "LH3" will be created.
 - **Validity**: it is one month by default.
 - **Quantity**: it is one instance by default.
3. Click **Buy Now**.
4. After confirming that the configuration information is correct, click **Submit Order** and make the payment as prompted.

After making the payment, the Lighthouse instance purchase will be successfully completed. Then, you can log in to the instance.

## Step 3. Log in to the Lighthouse Linux instance
Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), find the newly purchased instance in the instance list, and click **Log in**. 
You will log in to the Linux instance through a webshell terminal without entering the password.
![](https://main.qcloudimg.com/raw/71162a6e915198b66810b7919dfcdb66.png)





## Step 4. Reset the Lighthouse Linux instance password (optional)
If you want to use SSH or a remote login application to connect to the Linux instance, please reset the password or set a key first. This step takes resetting the password as an example. Please perform operations based on your actual needs.

1. In the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index), find the newly purchased instance in the server list and enter its details page.
2. In the **Instance Info** column, click **Reset Password** as shown below:

3. In the **Reset Password** pop-up window, enter and confirm the password as prompted.
>- The password can be reset only when the instance is shut down. We recommend you shut down the instance first before resetting the password. If you want to reset the password when the instance is running, you should select **Agree to a forced shutdown**.
>- If you use the Ubuntu image application to create an instance, the instance will disable login of the `root` username through password by default. If you need to enable it, please refer to [How do I log in to an instance with the root account on Ubuntu?](https://intl.cloud.tencent.com/document/product/1103/41257)
>


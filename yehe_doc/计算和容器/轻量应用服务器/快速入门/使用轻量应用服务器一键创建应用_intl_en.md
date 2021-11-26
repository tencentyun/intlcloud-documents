This document describes how to use Lighthouse to quickly create and deploy an application. 


## Step 1. Sign up
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/zh/document/product/378/17985) and complete identity verification.
If you already have a Tencent Cloud account, you can ignore this step.

## Step 2. Create a Lighthouse instance with an application image
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Click **Create** to enter the Lighthouse instance purchase page.
 - **Region**: we recommend you select a region near your target users to reduce the network latency and improve the access speed. For example, if your target users are in **Shenzhen**, you can select **Guangzhou** as the region.
 - **Image**: select the required application. This document uses the **WordPress 5.4.2** application image as an example.
 - **Instance Package**: select an instance package according to the required instance configuration (including CPU, memory, system disk, bandwidth or peak bandwidth, and monthly traffic).
 - **Instance Name**: enter a custom instance name. If it is left empty, "image name-four random characters" will be used as the name by default. When instances are created in batches, their names will be consecutive with auto-incrementing suffixes. For example, if you enter "LH" as the name and select 3 as the quantity, 3 instances "LH1", "LH2", and "LH3" will be created.
 - **Validity**: it is one month by default.
 - **Quantity**: it is one instance by default.
3. Click **Buy Now**.
4. After confirming that the configuration information is correct, click **Submit Order** and make the payment as prompted.

Make the payment to complete the creation. Then, you can log in to the instance and manage the application.

## Step 3. Get the admin information
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and select the newly created instance.
2. Select the **Application Management** tab to enter the application management details page.
3. [](id:Step3)In the **Application Software Info** column, click <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin:-3px 0px;"> to copy the command for getting the WordPress admin account and password.
4. In the **Application Software Info** column, click **Log in** as shown below:

5. [](id:Step5)In the pop-up login window, paste the command obtained in [step 3](#Step3) and press **Enter**.
Then, you can get the WordPress admin account (`admin`) and the corresponding password.

## Step 4. Manage the application
1. In the **Application Software Info** column, click **Admin Login Address** of WordPress.
2. In the opened browser window, enter the account and password obtained in the [step of getting the admin information](#Step5) and click **Log in**.
After successful login, you can manage, customize, and configure WordPress based on your actual needs as shown below:


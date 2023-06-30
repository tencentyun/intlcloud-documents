This document describes how to use Lighthouse to quickly create an application. You can create and deploy an application with speed and ease as instructed in this document.


## Step 1. Sign up and top up
1. [Sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/account/register).
If you already have a Tencent Cloud account, ignore this step.
2. [Top up](https://console.cloud.tencent.com/expense/recharge).
Lighthouse instances are available through monthly subscription. To make a purchase, you need to top up your account as instructed in [Payment Methods](https://intl.cloud.tencent.com/document/product/555/7425).

## Step 2. Select an application image during Lighthouse instance creation
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index).
2. Click **Create** to enter the Lighthouse purchase page.
![](https://qcloudimg.tencent-cloud.cn/raw/82022ca773e3abff0d828496aee778dd.png)
 - **Region**: We recommend you select a region near your target users to reduce the network latency and improve their access speed.
 - **Availability zone**: **Randomly assigned** is selected by default. You can select one as well.
 - **Image**: Select the required application. In this example, the **WordPress 5.7.1** application image is selected.
 - **Instance bundle**: Select an instance bundle according to the required instance configuration (including CPU, memory, system disk, bandwidth, and data transfer plan).
 - **Instance Name**: enter a custom instance name. If it is left empty, "image name-four random characters" will be used as the name by default. When instances are created in batches, their names will be consecutive with auto-incrementing suffixes. For example, if you enter "LH" as the name and select 3 as the quantity, 3 instances "LH1", "LH2", and "LH3" will be created.
 - **Purchase period**: Default to **1 month**.
 - **Quantity**: One instance by default.
3. Click **Buy now**.
4. Make sure the configuration information is correct, click **Submit order** and make the payment as prompted.

After making the payment, the WordPress application will be successfully created. Then, you can log in to the instance and manage the application.

## Step 3. Get the admin information
1. Log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse/instance/index) and select the target instance in the instance list to enter its details page.
2. Select the **Pre-installed application** tab, and enter the application details page.
<dx-alert infotype="notice" title="">
Only the Lighthouse instance created with "application image" has the **Pre-installed application** tab.
</dx-alert>
3. [](id:Step3)In the **Application Software Info** column, click <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin:-3px 0px;"> to copy the command for getting the WordPress admin account and password.
4. In the **Pre-installed software** section, click **Log in**.
![](https://qcloudimg.tencent-cloud.cn/raw/cc25dd3135a2de549a5b82fdcf4f7dd0.png)
5. [](id:Step5)In the pop-up login window, paste the command obtained in [step 3](#Step3) and press **Enter**.
Then, you can obtain WordPress admin account (admin) and password (wordpress_password).

## Step 4. Manage the application
1. In the **Pre-installed software** section, click **Admin address** of WordPress.
2. In the opened browser window, enter the account and password obtained in [Step 3. Get the admin information](#Step5) and click **Log in**.
After successful login, you can manage, customize, and configure WordPress based on your actual needs as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/b6b8135876fd75674a060229a8464a05.png)


## See Also
For more information on practical operations in different scenarios, see [Best Practices](https://intl.cloud.tencent.com/document/product/1103/41255).


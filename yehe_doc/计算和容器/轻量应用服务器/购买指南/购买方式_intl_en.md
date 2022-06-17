## Purchasing in Console
1. Log in to the [Lighthouse purchase page](https://buy.intl.cloud.tencent.com/lighthouse?buy_from=lh-console) and configure the following information as prompted:
![](https://qcloudimg.tencent-cloud.cn/raw/540a54ce93a72135d6e83e76917a767b.png)
 - **Region**: We recommend you select the region closest to your end users to minimize the access latency and improve the access speed.
 - **Availability zone**: **Randomly assigned** is selected by default. You can select one as well.
 <dx-alert infotype="notice" title="">
- Instances in the same region can communicate with each other over the private network. For applications with high disaster recovery requirements, deploy Lighthouse instances to different AZs in the same region to ensure fault isolation. Note that it may cause a higher communication latency.
- After creating an instance, you cannot change its AZ.
</dx-alert>
 - **Image**: You can choose application images, system images, Docker images, custom images, and shared images. For more information, see [Image](https://intl.cloud.tencent.com/document/product/1103/41261).
 - **Instance bundle**:Different bundles have different specifications of CPU, memory, SSD storage, bandwidth, and data transfer package. For more information, see [Basic Bundle Overview](https://intl.cloud.tencent.com/document/product/1103/41403).
 - **Instance name**: Enter a custom instance name. If it is left empty, the selected image name will be used as the name by default. When multiple instances are created in a batch, their names will be consecutive with auto-incrementing suffixes. For example, if you enter "LH" as the name and select 3 as the quantity, 3 instances "LH1", "LH2", and "LH3" will be created.
 - **Login method*: If you select a Windows image, you can use this option to set the login password of the instance:
    - **Set password**: Set the custom password for instance login.
    - **Random password**: The system sends an automatically generated password to your [Message Center](https://console.cloud.tencent.com/message).
 - **Purchase period**: It indicates the validity of the Lighthouse instance.
<dx-alert infotype="explain" title="">
You can select **Auto-renew the device every month when my account has sufficient balance** to enable the auto-renewal feature. After successfully creating an instance, you can modify the current auto-renewal settings as instructed in [Auto-Renewal](https://intl.cloud.tencent.com/document/product/1103/41559).
</dx-alert>
 - **Quantity**: It indicates the number of Lighthouse instances to be purchased.
3. Click **Buy now**.
4. Make sure the configuration information is correct, click **Submit order** and make the payment as prompted.
After making the payment, you can enter the [Lighthouse console](https://console.cloud.tencent.com/lighthouse) to check your Lighthouse instance. Generally, it takes 1-3 minutes to create an instance.




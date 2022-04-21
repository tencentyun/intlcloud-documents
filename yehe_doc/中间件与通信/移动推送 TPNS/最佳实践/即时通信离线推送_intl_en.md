## Overview

Offline message push allows your application to successfully receive pushed messages even when it is closed.
If your IM application needs to use offline message push, activate the TPNS service. After TPNS is activated and authorized, you can use it to push IM messages offline and collect related statistics.

>? TPNS provides free basic offline push service for IM customers. If you need to use various types of data statistics and more push types provided by TPNS, upgrade your IM SDK to the latest version (integrated with TPNS SDK) and purchase the TPNS paid service.
>

## Preparations

1. Prepare the following:
>? If you have configured vendor information (such as `channel_id` and the Tap-to-Redirect action) in IM, you do not need to create a new TPNS application. We will migrate IM vendor information to the TPNS application by April 15, 2022. Until then, you can still use the original offline message push capability.
>
 - Application package name
 - AppId, AppKey, and AppSecret allocated by the push platform of the Android vendor channel; iOS push certificate
2. Activate [TPNS](https://console.cloud.tencent.com/tpns) by using the same Tencent Cloud root account as that of the IM service.
>? TPNS does not charge authorized IM applications for offline message push.
>
3. Click **Create Product** to create a TPNS product.
4. In the pop-up window, enter the product name, set the product category, select the service access point, and click **Confirm**.
 ![](https://qcloudimg.tencent-cloud.cn/raw/c1a8c2d85023df3c3a570df335ca1ec9.png)
>? Select a service access point (data storage location) based on the service region of your application. For example, you can select Guangzhou and Shanghai for services inside the Chinese mainland, and select Hong Kong (China) and Singapore for services outside the Chinese mainland.
>


### Confirming authorization status

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns), select a target product, and click **Configure Now**.
2. On the left sidebar, click **Third party authorization**.
3. On the **Third-Party Service Authorization** page, change **TPNS Application Authorization** to **IM Application Authorization**.
![](https://qcloudimg.tencent-cloud.cn/raw/f1ae47e26d158971cea31971e6f503bc.png)
If you do not see the authorization mode change, check as follows:
 - Check whether an application is created in the IM service. If not, go to the [IM console](https://console.cloud.tencent.com/im) to create an IM application.
 - Check whether the current login account is an authorized sub-account. You are advised to switch to the root account.

### Adding authorization

1. If this is your first time entering the IM application authorization page, the page shown as follows is displayed. Click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/a9ab959211af631e177dc8d0571b38b1.png)
2. On the **Tencent Cloud Instant Messaging** page, click **Add Authorization**.
![](https://qcloudimg.tencent-cloud.cn/raw/081d3f59fc4969c6c27d0af331456070.png)
3. In the pop-up window, select the name of the IM application under the current account, select the name of the TPNS product created in **Preparations**, select a TPNS application name, and click **Submit**.
![](https://qcloudimg.tencent-cloud.cn/raw/86518daed240aa525976c47382ef96fe.png)
If an application has already been authorized, it cannot be selected, and you need to create another application or unauthorize the authorized application and authorize it again. 

### Viewing application status

If an application has been authorized to IM, check its status as follows:
1. Log in to the TPNS console and go to the [Product Management](https://console.cloud.tencent.com/tpns/product) page. You can see that the value of the application in **Service details** has changed to **IM push only (free)**.
![](https://qcloudimg.tencent-cloud.cn/raw/17a9e6af26f672194604e6cdfe9cfefb.png)
2. On the left sidebar, choose **Message Management** > **Push Plan**. You can see that a plan named **IM message** is automatically created.
![](https://qcloudimg.tencent-cloud.cn/raw/edd0044a0c90a588808b8af1be7f199a.png)


## Application Configuration

If you have configured vendor information in the IM service, data has been automatically synchronized, and you do not need to configure application settings. Otherwise, you need to configure the vendor channel (Android) or push certificate (iOS).

### Configuring the application package name

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns), select a target product, and click **Configure Now**.
2. On the left sidebar, choose **Message Management** > **Basic Config**, enter the application package name obtained in **Preparations**, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/4d1bb146b930a50f6183c6f876c737ee.png)

### Configuring the Android vendor channel

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns), select a target product, and click **Configure Now**.
2. On the left sidebar, choose **Message Management** > **Basic Config** to go to the basic configuration page.
3. In the **Vendor Channel** area, click ![](https://qcloudimg.tencent-cloud.cn/raw/020b986ff803b9eadd8b68677514c774.png) corresponding to a vendor channel, enter the AppId, AppKey, and AppSecret obtained in **Preparations**, and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/fd151e8889b30c82326404bbf981ae56.png)


### Configuring the iOS push certificate

1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns), select a target product, and click **Configure Now**.
2. On the left sidebar, choose **Message Management** > **Basic Config** to go to the basic configuration page.
3. In the **Push Certificate** area, click **Upload Certificate** and upload the certificate as instructed.
![](https://qcloudimg.tencent-cloud.cn/raw/0b2b4512481d58a946fbe93beb561d00.png)
After the certificate is submitted, the uploaded certificate is displayed. For how to acquire a certificate, see [Acquisition of Push Certificate](https://intl.cloud.tencent.com/document/product/1024/30728).

### Viewing offline message statistics

After completing configuration, you can view the corresponding offline message sending history.
1. Log in to the [TPNS console](https://console.cloud.tencent.com/tpns).
2. On the left sidebar, choose **Message Management** > **Push Plan**, and click **Details** corresponding to the IM message plan to view the offline message sending history.
![](https://qcloudimg.tencent-cloud.cn/raw/c88a8437c43fabfa3702b63bccf8bc73.png)


## Notes

- An authorized IM application cannot be deleted directly. It needs to be unauthorized via third-party authorization first.

- An authorized IM application service includes only the offline push feature. If you need to use other push services and data statistics, you need to enable them as instructed.

  ![](https://qcloudimg.tencent-cloud.cn/raw/a303a81693285f4df1b2807119921d6b.png)
  
  ![](https://qcloudimg.tencent-cloud.cn/raw/0a11565a13309973aad6b5cf912769a9.png)

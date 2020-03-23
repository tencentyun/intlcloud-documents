

To help you analyze the full-linkage message push effect, TPNS supports display of arriving data through vendor-specific channels. The support for callback of arriving data varies by vendor in China, and data of some channels cannot be directly obtained without corresponding configuration.

After successfully configuring the arriving data display feature, you can view the push conversion data in push details in the TPNS Console or get it by using a TPNS RESTful API.

## Overview

| Vendor-specific Channel | Arrival Callback Supported | Configuration Required |
| -------- | ---------------- | ------------ |
| Huawei channel | Yes               | Yes           |
| Mi channel | Yes               | No           |
| OPPO channel | Yes               | No           |
| Vivo channel | Yes               | No           |
| Meizu channel | No               | Yes           |

## Configuration Guide

The acquisition of arriving data through the Huawei channel needs to be configured by yourself. For more information on how to configure it, please see [Message Receipt](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/push-receipt#h1-1575515478691) on the Huawei Developer Platform. The configuration process is as follows:

### Enabling receipt permission

1. Log in to [AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html) and select **My App**.
![](https://main.qcloudimg.com/raw/d625fe7e497f2bbe0aff0a881a21dc15.png)    
2. Select the product name of your app for which you want to activate the push service to enter the app information page.
3. Click the **Develop** tab and select **Growing** > **Push Service** on the left sidebar.
4. In the service status section, click **Activate**. After the service is activated, you can select whether to enable receipt.
![](https://main.qcloudimg.com/raw/07a9ae9fc123f6e86fe4ddff5b4de721.png)

### Configuring receipt parameters

1. Configure the message receipt callback address as described below:
  - Cluster in Guangzhou: https://api.tpns.tencent.com/log/statistics/hw
  - Cluster in Hong Kong (China): https://api.tpns.hk.tencent.com/log/statistics/hw
  - Cluster in Singapore: https://api.tpns.sgp.tencent.com/log/statistics/hw
2. Configure the HTTPS certificate. Click [here](https://api.tpns.tencent.com/v3/tpnscert/download) to download it.
3. Configure the callback username and key (optional) for authentication.
4. Click **Test Receipt** to test the receipt address.
>Currently, if you click **Test Receipt**, the error message "Certificate error. Please modify and upload it again" will be displayed. Ignore it and click **Submit**.

5. Click **Submit** to activate the service.
![](https://main.qcloudimg.com/raw/d58a7ef52c34e9356a870607cfd9794f.png)

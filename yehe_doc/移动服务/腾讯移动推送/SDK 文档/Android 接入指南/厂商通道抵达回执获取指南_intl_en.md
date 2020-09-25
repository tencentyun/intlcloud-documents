To help you analyze the full-linkage message push effect, TPNS supports display of arriving data through vendor channels. The support for receipt of arriving data varies by vendor in China, and data of some channels cannot be directly obtained without corresponding configuration.

After successfully configuring the arriving data display feature, you can view the push conversion data in push details in the TPNS Console or get it by using a TPNS RESTful API.

## Overview

| Vendor Channel | Arrival Supported | Configuration Required |
| -------- | ---------------- | ------------ |
| Huawei channel | Yes               |**Yes**           |
| Meizu channel | Yes               |**Yes**           |
| Mi channel | Yes               | No           |
| OPPO channel | Yes               | No           |
| Vivo channel | Yes               | No           |
| FCM channel | Yes | No |

>?Vendor channel arrival receipt data is for reference only.

## Receipt Configuration Guide for Huawei Channel

After integrating the SDK for Huawei Channel, you need to activate and configure message receipt on the Huawei open push platform before the arrival data for the Huawei channel can be obtained. For detailed directions, please see [Message Receipt](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/push-receipt#h1-1575515478691). The configuration steps are as follows:

### Enabling receipt permission

1. Log in to [AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html) and select **My App**.
![](https://main.qcloudimg.com/raw/59521f7425a5d6e1bccae726635096dc.png)    
2. Select the product name of your application for which you want to activate the push service to enter the application information page.
3. Click the **Develop** tab and select **Growing** > **Push Service** on the left sidebar.
4. In the service status section, click **Activate**. After the service is activated, you can select whether to enable receipt.
![](https://main.qcloudimg.com/raw/32556c2eb1d74756583cc8c27d436883.png)

### Configuring receipt parameters

1. Configure the message receipt address. Please view the service access point of your application in the [TPNS Console](https://console.cloud.tencent.com/tpns) and select the receipt address of the corresponding service access point for configuration:
![](https://main.qcloudimg.com/raw/ccdcd39ece57703af3106fa756f98991.png)
<table>
 <tbody><tr>
 <th>Service access point</th>
 <th>Callback address</th> 
 </tr>
 <tr>
 <td >Service access point in Guangzhou</td>
 <td>https://stat.tpns.tencent.com/log/statistics/hw</td>
 </tr>
 <tr>
 <td>Service access point in Hong Kong (China)</td>
 <td>https://stat.tpns.hk.tencent.com/log/statistics/hw</td>
 </tr>
 <tr>
 <td>Service access point in Singapore</td>
 <td>https://stat.tpns.sgp.tencent.com/log/statistics/hw</td>
 </tr>
 <tr>
 <td>Service access point in Shanghai</td>
 <td>https://stat.tpns.sh.tencent.com/log/statistics/hw </td>
 </tr>
 </tbody></table>
 </tbody></table>
2. Configure the HTTPS certificate. Click [here](https://api.tpns.tencent.com/v3/tpnscert/download) to download it.
3. Configure the username and key (optional) for authentication.
4. Click **Test Receipt** to test the receipt address.
>!Currently, if you click **Test Receipt**, the error message "Failed to test the callback address" will be displayed. Ignore it and click **Submit**.

5. Click **Submit** to activate the service.
![](https://main.qcloudimg.com/raw/98a53519ef466977928ebfc1eac879fa.png)

## Receipt Configuration Guide for Meizu Channel

After integrating the SDK for Meizu Channel, you need to create a receipt on the Flyme push platform and activate it in the TPNS Console before the arrival data for the Meizu channel can be obtained. The configuration steps are as follows:
>!You need to complete both the following steps; otherwise, delivery through the Meizu channel may fail.

### Configuring receipt

1. Log in to the [Flyme Push Platform](https://open.flyme.cn/open-web/views/push.html), select the application for which to configure the receipt, and click **Open Application**.
2. On the push notification page, click **Configuration Management** > **Receipt Management**.
3. Enter the receipt address in **Create Receipt**. Please view the service access point of your application in the [TPNS Console](https://console.cloud.tencent.com/tpns) and select the receipt address of the corresponding service access point for configuration:
![](https://main.qcloudimg.com/raw/a7940ac0e3a6d8c68523cce9d8483d22.png)
<table>
 <tbody><tr>
 <th>Service access point</th>
 <th>Callback address</th> 
 </tr>
 <tr>
 <td rowspan="2">Service access point in Guangzhou</td>
 <td>https://api.tpns.tencent.com/log/statistics/mz</td>
 </tr>
 <tr>
 <td>https://stat.tpns.tencent.com/log/statistics/mz</td> 
 </tr>
 <tr>
 <td>Service access point in Hong Kong (China)</td>
 <td>https://stat.tpns.hk.tencent.com/log/statistics/mz</td>
 </tr>
 <tr>
 <td>Service access point in Singapore</td>
 <td>https://stat.tpns.sgp.tencent.com/log/statistics/mz </td>
 </tr>
 <tr>
 <td>Service access point in Shanghai</td>
 <td>https://stat.tpns.sh.tencent.com/log/statistics/hw </td>
 </tr>
 </tbody></table>
  
  >! Both callback addresses for service access point in Guangzhou are required.
4. After entering the receipt address, click **Add** on the right, and if the newly created receipt is correctly displayed in the **Receipt List**, the configuration is successful.

### Activating receipt
1. Go to the [Product Management](https://console.cloud.tencent.com/tpns) page, select the application to be activated, and click **Configuration Management**.
![](https://main.qcloudimg.com/raw/7ac8c31f122ae267796672f50a10b55f.png)
2. On the configuration management page, click the edit icon in **Vendor Channel** > **Meizu Official Push Channel**.
![](https://main.qcloudimg.com/raw/f12fc508aca29874b4d70afdc365b6c8.png)
3. On the Meizu official push channel editing page, click **Activate Now**.
![](https://main.qcloudimg.com/raw/6c6c40c0f4867e118b54ebdb7083a7f9.png)


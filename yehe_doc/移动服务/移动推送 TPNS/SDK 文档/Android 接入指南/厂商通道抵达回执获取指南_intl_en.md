To help you analyze the full-linkage message push effect, TPNS supports the display of message arrival receipts for vendor channels. The support for message arrival receipts varies with the vendor channel inside the Chinese mainland. The message arrival receipts of certain channels cannot be directly obtained without corresponding configuration.

After successfully configuring the message arrival receipt display feature, you can view the push conversion data in push details in the TPNS console or obtain the push conversion data through a TPNS RESTful API.

## Overview

| Vendor Channel | Support for Arrival Receipt | Require Configuration |
| --------- | ------------ | ------------ |
| Huawei channel | Yes               | **Yes**           |
| Meizu channel  | Yes           | **Yes**          |
| Mi channel | Yes               | No           |
| OPPO channel | Yes               | No           |
| vivo channel | Yes               | No           |
| FCM channel  | Yes           | No           |

>? The arrival receipt information of vendor channels is for reference only.
>

## Receipt Configuration Guide for the Huawei Channel

After integrating the Huawei channel SDK, you need to enable and configure the message receipt feature on the Huawei Developer Platform so that the arrival receipts of the Huawei channel can be obtained. For configuration details, see [Message Receipt](https://developer.huawei.com/consumer/cn/doc/development/HMS-Guides/push-receipt#h1-1575515478691). The configuration process is as follows.

### Enabling the message receipt feature

1. Log in to [AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html) and select **My apps**.
![](https://main.qcloudimg.com/raw/59521f7425a5d6e1bccae726635096dc.png)
2. Select the parent product name of the application for which the service is to be enabled. The application information page is displayed.
3. On the application information page, choose **All services** > **Push Kit**.
4. On the **Push Kit** page, click **Enable** corresponding to **Receipt status**.
![](https://main.qcloudimg.com/raw/32556c2eb1d74756583cc8c27d436883.png)

### Setting receipt parameters

1. Set the message receipt address. Please view the service access point of your application in the [TPNS console](https://console.cloud.tencent.com/tpns) and select the corresponding receipt address for configuration.
![](https://main.qcloudimg.com/raw/fbd7bb014dc5fa8bd1b2323471671e59.png)
<table>
 <tbody><tr>
 <th>Service Access Point </th>
 <th>Receipt Address </th> 
 </tr>
 <tr>
 <td >Guangzhou </td>
 <td>https://stat.tpns.tencent.com/log/statistics/hw/AccessID  </td>
 </tr>
 <tr>
 <td>Hong Kong (China) </td>
 <td>https://stat.tpns.hk.tencent.com/log/statistics/hw/AccessID </td>
 </tr>
 <tr>
 <td>Singapore </td>
 <td>https://stat.tpns.sgp.tencent.com/log/statistics/hw/AccessID </td>
 </tr>
 <tr>
 <td>Shanghai </td>
 <td>https://stat.tpns.sh.tencent.com/log/statistics/hw/AccessID </td>
 </tr>
 </tbody></table>

> ?Replace **AccessID** in the addresses with the access ID of your application. For example, if your application uses the Guangzhou service access point, set the receipt address to `https://stat.tpns.tencent.com/log/statistics/hw/1500016691`. 

2. Download the HTTPS certificate corresponding to the service access point of your application. Use a text editor to open the certificate file and copy the certificate to the certificate text box.
<table>
 <tbody><tr>
 <th>Service Access Point </th>
 <th>Download Address </th> 
 </tr>
 <tr>
 <td >Guangzhou </td>
 <td><a href="https://tpns-1259470370.cos.ap-guangzhou.myqcloud.com/tpnshttpscert/tpns-https-cert/tpns-gz1.crt">Download</a></td>
 </tr>
 <tr>
 <td>Hong Kong (China) </td>
 <td><a href=" https://tpns-1259470370.cos.ap-guangzhou.myqcloud.com/tpnshttpscert/tpns-https-cert/tpns-hk.crt">Download</a> </td>
 </tr>
 <tr>
 <td>Singapore </td>
 <td><a href="https://tpns-1259470370.cos.ap-guangzhou.myqcloud.com/tpnshttpscert/tpns-https-cert/tpns-sgp.crt">Download</a> </td>
 </tr>
 <tr>
 <td>Shanghai </td>
 <td><a href=" https://tpns-1259470370.cos.ap-guangzhou.myqcloud.com/tpnshttpscert/tpns-https-cert/tpns-sh.crt">Download</a> </td>
 </tr>
 </tbody></table>
3. Configure the callback username and key (optional) for authentication.
4. Click **Test Receipt** to test the receipt address.
> !Currently, if you click **Test Receipt**, the error message "Failed to test the callback address" will be displayed. Ignore it and click **Submit**.
5. Click **Submit** to activate the service.
![](https://main.qcloudimg.com/raw/98a53519ef466977928ebfc1eac879fa.png)

## Receipt Configuration Guide for the Meizu Channel

After integrating the Meizu channel SDK, you need to create a receipt on the Flyme push platform and activate it in the TPNS console so that the arrival receipt of the Meizu channel can be obtained. The configuration process is as follows.

> !You need to complete both the following steps; otherwise, delivery through the Meizu channel may fail.

### Configuring a receipt

1. Log in to the [Flyme Push Platform](https://open.flyme.cn/open-web/views/push.html), select the application for which a receipt is to be configured, and click **Open Application**.
2. On the push notification page, choose **Configuration Management** > **Receipt Management**.
3. Enter the receipt address in **Create Receipt**. Please view the service access point of your application in the [TPNS console](https://console.cloud.tencent.com/tpns) and select the corresponding receipt address for configuration.
   ![](https://main.qcloudimg.com/raw/a7940ac0e3a6d8c68523cce9d8483d22.png)
	
	<table>
	 <tbody><tr>
	 <th>Service Access Point </th>
	 <th>Receipt Address </th> 
	 </tr>
	 <tr>
	 <td rowspan="2">Guangzhou </td>
	 <td>https://api.tpns.tencent.com/log/statistics/mz  </td>
	 </tr>
	 <tr>
	 <td>https://stat.tpns.tencent.com/log/statistics/mz </td> 
	 </tr>
	 <tr>
	 <td>Hong Kong (China) </td>
	 <td>https://stat.tpns.hk.tencent.com/log/statistics/mz </td>
	 </tr>
	 <tr>
	 <td>Singapore </td>
	 <td>https://stat.tpns.sgp.tencent.com/log/statistics/mz </td>
	 </tr>
		<tr>
	 <td>Shanghai </td>
	 <td>https://stat.tpns.sh.tencent.com/log/statistics/mz </td>
	 </tr>
 </tbody></table>

> ?For the Guangzhou service access point, both receipt addresses must be entered.

4. After entering the receipt address, click **Add** on the right. If the newly created receipt is correctly displayed in **Receipt List**, the configuration is successful.



### Activating the receipt

1. Go to the [Product Management](https://console.cloud.tencent.com/tpns) page, select the application for which a receipt is to be activated, and click **Configuration Management**.
   ![](https://main.qcloudimg.com/raw/7ac8c31f122ae267796672f50a10b55f.png)
2. On the configuration management page, click the edit icon in **Vendor Channel** > **Meizu Official Push Channel**.
   ![](https://main.qcloudimg.com/raw/f12fc508aca29874b4d70afdc365b6c8.png)
3. On the Meizu official push channel editing page, click **Activate Now**.
   ![](https://main.qcloudimg.com/raw/6c6c40c0f4867e118b54ebdb7083a7f9.png)


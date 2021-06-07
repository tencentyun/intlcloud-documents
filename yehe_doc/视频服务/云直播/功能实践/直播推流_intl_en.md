The nature of CSS is a streaming process, similar to the live broadcast of TV channels sent to audience through cable networks. In order to complete this process, CSS needs to have a capture and push device (similar to a camera), a cloud live streaming service (similar to a cable network), and a playback device (similar to a TV set). These devices can be smart devices such as mobile phones, PCs, and tablets as well as web browsers. We provide complete software demos for different types of devices.

[](id:step1)
## Preparations
1. Activate the [CSS service](https://console.cloud.tencent.com/live?from=product-banner-use-lvb).
2. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click **Add Domain Name** to add an ICP filed push domain name. For more information, please see [Adding Domain Name](https://intl.cloud.tencent.com/document/product/267/35970).
>? CSS provides a default push domain name in the format of `xxx.livepush.myqcloud.com`. We recommend you not use it as the push domain name for your real business.

[](id:push_add)
## Getting Push Address
Log in to the CSS console, select **CSS Toolkit** > **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** to generate a push address and configure as follows:
- Select **push domain name** as the type of address to generate.
- Select the push domain name you added in domain management.
- Enter an `AppName` (`live` by default). This is used to differentiate the paths of different applications under the same domain name.
- Enter a custom `StreamName`, such as `liveteststream`.
- Select the expiration time of the address, such as `2019-10-18 23:59:59`.
- Click **Generate Address**. 

>!
>- To ensure the security of your live streams, the system will automatically enable push authentication. You can also select the push domain name to be modified in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click **Manage** on the right to enter the domain name details page and customize the authentication information in **Push Configuration**. The push address is in the following format:
`rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)`
>- In addition to the above method, you can also select a push domain name in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the CSS console, click **Manage**, select **Push Configuration**, enter the expiration time of the push address and the custom `StreamName`, and click **Generate Push Address** to generate a push address.
>-If you need a **persistent push address**, you can enter **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, select a push domain name, click **Manage**, and select **Push Configuration** for calculation and generation by referring to the sample code in **Push Address Sample Code**. For more information, please see [How can I view the push sample code?](https://intl.cloud.tencent.com/document/product/267/31059).

[](id:live_push)
## CSS Push
You can use the following methods to implement CSS push based on your business scenario:

[](id:pc)
### Scenario 1. PC push
For PC (Windows/macOS), you can choose to install [OBS](https://obsproject.com/download) or [XSplit](https://www.xsplit.com/zh-cn) for push. The former is a free open-source video recording and streaming program that supports operating systems such as Windows, macOS, and Linux, while the latter is a paid program that offers a standalone installer for live game streaming. For non-game live streaming, we recommend you use BroadCaster.
![](https://main.qcloudimg.com/raw/dcb203971ac99415258ea0b0ee1529a8.png)
This document uses push with OBS as an example to describe the steps. Assume that the prepared push address is:

```
rtmp://3891.livepush.myqcloud.com/live/3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F
```


1. Go to [OBS official website](https://obsproject.com/download) to download and install the push tool.
2. Open OBS and click **Controls** > **Settings** at the bottom to enter the settings page.
3. Click **Stream** to enter the push configuration page and set as follows:
  1. Select "Custom" as the service type.
  1. Enter the first half of the push address as the server, such as `rtmp://3891.livepush.myqcloud.com/live/`.
  1. Enter the second half of the push address as the stream key, such as `3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F`.
  1. Click **OK** in the bottom-right corner.
![](https://main.qcloudimg.com/raw/7b5365a0be590c3694fbb6d0ded8e5e3.png)
4. Click **Controls** > **Start Streaming** to test streaming. For more information on how to use OBS, please see [Push via OBS](https://intl.cloud.tencent.com/document/product/267/31569).

[](id:web)
### Scenario 2. Web push
1. Log in to the CSS console.
2. Select **Auxiliary Tools** > **[Web Push](https://console.cloud.tencent.com/live/tools/webpush)**.
3. Perform the following settings on the web push page:
  1. Select a push domain name.
  2. Enter an `AppName` (`live` by default). This is used to differentiate the paths of different applications under the same domain name.
  2. Enter a custom `StreamName`, such as `liveteststream`.
  3. Select an expiration time, such as `2019-10-30 23:59:59`.
  4. Click **Start Push** and grant the camera permission to start the push.

>! The web push feature requires that your device have a camera installed and its browser support the Flash plugin to call the camera permission.

![](https://main.qcloudimg.com/raw/9da7489bb2387049859131e792364124.png)

[](id:mobile)
### Scenario 3. Mobile push
1. Scan the QR code with a mobile phone to download and install the [Video Cloud Toolkit](https://intl.cloud.tencent.com/document/product/1071/38147).
2. Open the toolkit and select **MLVB** > **Camera Push**.
3. Enter the [push address](#step1) manually or by scanning the QR code.
4. Tap **Start** in the bottom-left corner to start the push.

>? If you did not prepare a push address in advance, you can tap **New** on the right of the push address bar on the **Camera Push** page, and the system will automatically enter a push address and provide the corresponding playback address which can be used for CSS playback.

[](id:sdk)
### Scenario 4. CSS SDK push
If you need to integrate only CSS push into your existing application, follow the steps below:
1. Download the [MLVB SDK](https://intl.cloud.tencent.com/document/product/1071/38150).
2. Complete the integration as instructed in the [iOS](https://intl.cloud.tencent.com/document/product/1071/38157) or [Android](https://intl.cloud.tencent.com/document/product/1071/38158) integration document.

The CSS SDK is a collection of mobile live streaming services. It demonstrates in the form of free source code how to use Tencent Cloud CSS, VOD, IM, and COS to build the most appropriate live streaming solution for your business. For more information, please see [MLVB](https://intl.cloud.tencent.com/product/mlvb). 


## FAQs
- [How can I implement CSS playback?](https://intl.cloud.tencent.com/document/product/267/31559)
- [How can I splice a push URL?](https://intl.cloud.tencent.com/document/product/267/38393)
- [How can I calculate a hotlink protection URL?](https://intl.cloud.tencent.com/document/product/267/31560)


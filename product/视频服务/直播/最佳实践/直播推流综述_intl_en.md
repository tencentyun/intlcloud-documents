
## Preparations
1. Activate Tencent Cloud LVB: If you have not done so yet, click [Apply for Activation](https://cloud.tencent.com/product/lvb).
2. Add an LVB push domain name: LVB provides you with a default push domain name in the format of `xxx.livepush.myqcloud.com`. You can also add your own domain names that have obtained ICP filing. For more information, see [Domain Name Management](https://cloud.tencent.com/document/product/267/30559).
3. You need to generate a push address before a live broadcast can be started. Log in to the LVB Console, click **Domain Management**, select the added push domain name, and click **Manage** > **Push Configuration** > **Generate Push URL** to generate a push address. If you do not enable push authentication, the push address format is `rtmp://domain/live/StreamName`; otherwise, the format is `rtmp://domain/live/StreamName?txSecret=xxx&txTime=xxx`. For the sake of security of your live broadcast, it is highly recommended that you enable push authentication.
![](https://main.qcloudimg.com/raw/f0e167bde77dfc23a52ce48b4078a57f.png)
![](https://main.qcloudimg.com/raw/4feffd90e98c0fdf1ce0fccf78f9a360.png)

## Mobile Push

You can use the Video Cloud Toolkit provided by Tencent Cloud, WeChat Mini Program, and MLVB SDK for mobile push and playback.

### Video Cloud Toolkit
#### Preparations
1. You need to install the Video Cloud Toolkit on two mobile phones, one for push and one for playback at the same time.
2. You can scan the following QR code with WeChat or QQ to install the Mobile Video Cloud Toolkit for trial. For more information, see [MLVB SDK Demo](https://cloud.tencent.com/document/product/454/6555).
![](https://main.qcloudimg.com/raw/9236fd4de1388ed9f0eb1fee89629989.jpg)

#### Push
1. Get a push address.
  - You can get a push address in the console.
  - You can also get one on the mobile phone. Launch the Video Cloud Toolkit and select **Camera Push** in **MLVB**.
	![](https://main.qcloudimg.com/raw/d7fbb9eeaf991f01c5c3d408344861c1.png)
  Tap **New** to the right of the push address bar on the Camera Push page, and the system will automatically create a push address and generate four QR codes of the playback address (which will be automatically copied to the clipboard, and you can paste it into the player or scan a QR code to watch the video), as shown below:
	![](https://main.qcloudimg.com/raw/1e3919416f543ca923fc597eeb1fd61d.png)
2. Tap the leftmost Play icon to start the push.

#### Playback
1. Get a playback address.
 - You can get a playback address in the console. For more information, see [Configure Playback Domain Name](https://cloud.tencent.com/document/product/267/20381) in Domain Name Management.
 - You can also enter the playback address that was automatically generated when you started the push just now or scan a system-generated QR code for playback.
2. Launch the Video Cloud Toolkit in the Demo, select **LVB Pull** in **MLVB** and enter the playback address you just obtained into the address bar as shown below:
	![](https://main.qcloudimg.com/raw/43cffe87d6dd6c135949c97de178d083.png)
3. Tap the leftmost Play icon to start the playback.


### WeChat Mini Program
#### Preparations
1. You need to launch the **Video Cloud Toolkit** WeChat Mini Program on two mobile phones, one for push and one for playback at the same time.
2. You can scan the following QR code with WeChat for trial. For more information, see [MLVB SDK](https://cloud.tencent.com/document/product/454/6555).
![](https://main.qcloudimg.com/raw/eff345d96146aad6a75cb7cec448b1d1.jpg)


#### Push
1. Get a push address.
	- You can log in to the LVB Console to get a push address.
	- You can also get one in the "Tencent Video Cloud" WeChat Mini Program. Launch the Mini Program, select **RTMP Push**, tap **Auto Generate** to the right of the push address on the RTMP page, and the system will automatically create a push address and generate a playback address as shown below:
![](https://main.qcloudimg.com/raw/569e1a2e77d794440710cce77ea8488a.jpg)
2. Tap **Start** in the middle to start the push.

#### Playback
1. Get a playback address.
	- You can get a playback address in the console. For more information, see [Configuring a Playback Domain Name](https://cloud.tencent.com/document/product/267/20381) in Domain Name Management.
	- You can also use the online QR code generator to generate a QR code for the playback address automatically generated during the push just now.
2. Launch the "Tencent Video Cloud" WeChat Mini Program and tap **Scan a Code** in **LVB Playback** to scan the QR code just generated as shown below:
![](https://main.qcloudimg.com/raw/99cfa9c49ebb705f6cff1ebeb4b3a66b.jpg)
3. Tap the leftmost Play icon to start the playback.


### LVB SDK
If you need to integrate only LVB Push into your existing app, follow the steps below to do so quickly.
1. Activate [LVB](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Flive).
2. Download the [MLVB SDK](https://cloud.tencent.com/document/product/454/7873).
3. Complete the access as instructed in the [iOS](https://cloud.tencent.com/document/product/454/7879) or [Android](https://cloud.tencent.com/document/product/454/7885) access document.


The LVB SDK is a collection of mobile live broadcasting services. It demonstrates in the form of free source code how to use Tencent Cloud LVB, VOD, IM, and COS to build the most appropriate live broadcasting solution for your business. For more information, see [MLVB](https://cloud.tencent.com/product/mlvb).

## PC Push

  You can use third-party push programs OBS (recommended) or XSplit on PC (Windows/Mac) to push compressed and encoded audio and video streams of various types such as live event, education, presentation, and gaming to the push address in Tencent Video Cloud, and viewers can watch the live content in real time at the playback address corresponding to the push address.
	 ![](https://main.qcloudimg.com/raw/67cdbb198cbdaf68d63f2993f12a8d17.png)
	
### Preparations Before Starting a Live Broadcast
#### Installing OBS
Download an appropriate installer at [OBS' official website](https://obsproject.com/download) and then install it with default settings. Windows, Mac, and Linux are supported. Make sure that the downloaded program is Open Broadcaster Software. OBS Studio is also available which is not covered in this document though.
#### Install XSplit
You can also download an installer at [XSplit's official website](https://www.xsplit.com/zh-cn) and then install it with default settings. XSplit is a paid tool. If your budget is low, use OBS (free). XSplit has a separate installer for live game broadcasting. For non-game live broadcasting, BroadCaster is recommended.

### Push
1. Log in to the [LVB Console](https://cloud.tencent.com/login?s_url=https%3A%2F%2Fconsole.cloud.tencent.com%2Flive).
2. Click **Domain Management** and select the push domain name you created.
3. Use the push address generator in **Manage** > **Push Configuration**.
4. Enter the **expiration time** and **StreamName**.
5. Click **Generate Push URL**.
6. Set the push address:
 - Assume that the prepared push address is:
```
rtmp://3891.livepush.myqcloud.com/live/3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F
```
 - It needs to be set in two parts:
	 - The first half of the push address is ` rtmp://3891.livepush.myqcloud.com/live/`, which is commonly referred to as an FMS URL.
	 - The second half of the push address is `3891_test?bizid=3891&txSecret=xxx&txTime=58540F7F`, which is commonly referred to as a stream code.
 - OBS push address setting:
	 For more information on the usage and settings of the OBS push tool, see [OBS Push](https://cloud.tencent.com/document/product/267/32726).
The OBS used here is v19.0.3. Click **Settings** in the bottom-right corner, select **Stream**, and then configure the stream type as **Custom Streaming Server**, the URL as the first half of the push address, and the stream key as the second half of the push address.
![](https://main.qcloudimg.com/raw/e6ae494cf56cca6025951f8507d78d08.jpg)


### Playback
1. Confirm the playback address which you can get in the console. For more information, see [Best Practices - LVB Playback](https://cloud.tencent.com/document/product/267/32733).
2. Download [VLC](http://www.videolan.org/vlc/) and install it with default settings.
3. For more information, see [VLC Player](https://cloud.tencent.com/document/product/267/32727).
![](https://main.qcloudimg.com/raw/4f53fbc0a0c559d849e8379e3d1374f1.jpg)
4. Or, download the [MLVB SDK](https://cloud.tencent.com/document/product/454/6555), use the online QR code generator to generate a QR code for the playback address, and then you can scan the code for playback.

## FAQs
**How to automatically splice the push address on the backend?**
   See [FAQs - How to splice a push URL?](https://cloud.tencent.com/document/product/267/32720).

**How is a hotlink protection URL calculated?**
    See [Best Practices - Hotlink Protection URL Calculation](https://cloud.tencent.com/document/product/267/32735).
  


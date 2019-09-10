
## Preparations
1. Activate Tencent Cloud LVB: If you have not done so yet, click [Apply for Activation](https://intl.cloud.tencent.com/product/lvb).
2. Add an LVB push domain name: LVB provides you with a default push domain name in the format of `xxx.livepush.myqcloud.com`. You can also add your own domain names that have completed ICP filing. 
3. You need to generate a push address before a live broadcast can be started. Log in to the LVB Console, click **Domain Management**, select the added push domain name, and click **Manage** > **Push Configuration** > **Generate Push URL** to generate a push address. If you do not enable push authentication, the push address format is `rtmp://domain/live/StreamName`; otherwise, the format is `rtmp://domain/live/StreamName?txSecret=xxx&txTime=xxx`. We recommend enabling push authentication to ensure the security of the live broadcast.
![](https://main.qcloudimg.com/raw/5fd6f9e06c5b40ea6b267bfa4c991e4b.png)
![](https://main.qcloudimg.com/raw/3b3d01d91791dcf65fc7958792e9ceb2.png)

## PC Push

  You can use third-party push programs OBS (recommended) or XSplit on PC (Windows/Mac) to push compressed and encoded audio and video streams of various types such as live event, education, presentation, and gaming to the push address in Tencent Video Cloud, and viewers can watch the live content in real time at the playback address corresponding to the push address.
	 ![](https://main.qcloudimg.com/raw/dcb203971ac99415258ea0b0ee1529a8.png)
	

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
![](https://main.qcloudimg.com/raw/7b5365a0be590c3694fbb6d0ded8e5e3.png)


### Playback
1. Confirm the playback address which you can get in the console. For more information, see [Best Practices - LVB Playback](https://intl.cloud.tencent.com/document/product/267/31559).
2. Download [VLC](http://www.videolan.org/vlc/) and install it with default settings.

## FAQs

**How is a hotlink protection URL calculated?**
    See [Best Practices - Hotlink Protection URL Calculation](https://intl.cloud.tencent.com/document/product/267/31560).



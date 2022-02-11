CSS allows you to push streams over the web. You can generate a push URL quickly and push streams from the camera or screen or push a local file to test CSS features.

## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- You have added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970).
- Your device has a camera installed and your browser allows Flash to access the camera.

## Directions
1. Log in to the CSS console and select **[Web Push](https://console.cloud.tencent.com/live/tools/webpush)**.
2. **Select the capturing source**, which can be camera, screen, or local file.
<dx-tabs>
::: Camera
Capture and publish audio/video from the camera/mic (which can be a peripheral device). Click **Turn On** for **Camera**/**Mic**. You need to grant your browser access to the camera/mic if it is the first time you perform this action.
![](https://qcloudimg.tencent-cloud.cn/raw/c5585e8a4ce99d65ace7af7c63e39487.png)
:::
::: Screen Sharing
 Capture and publish streams from the screen. Click **Select Screen** to select a screen/window/browser tab to publish.
![](https://qcloudimg.tencent-cloud.cn/raw/75d18898089e060dc118656c539d05a3.png)
:::
::: Local File
Publish a local file using the web push tool to CSS. Click **Select** to select a file to publish. Currently, you can publish only files in MP4 format.
![](https://qcloudimg.tencent-cloud.cn/raw/f1ae8270626dfe6cf0cbc822a907698e.png)
:::
</dx-tabs>
>! You cannot change the capturing source after enabling camera preview or selecting screen content to share. To switch the source, disable camera preview or cancel screen sharing first.
3. **Configure capturing data**. The defaults are recommended settings, which vary with resolution. You can click **Edit** and select **Custom** to customize capturing data. **For camera and screen sharing, the settings include resolution, video frame rate, and audio sample rate, while for local files, only the former two are applicable.**
![](https://qcloudimg.tencent-cloud.cn/raw/f126b1bf7035562517d8b6cf62c71cb0.png)
4. **Configure push data**. The defaults are recommended settings (the recommended video bitrate varies with resolution, and the audio bitrate is fixed). You can click **Edit** and select **Custom** to customize video and audio bitrates.
>? WebRTC push uses the Opus audio codec, and you are advised to play the streams pushed using LEB WebRTC URLs. If you use a standard live streaming protocol (RTMP, FLV, or HLS), the system will automatically convert the streams to AAC, which will incur transcoding fees. For details, see the [billing document](https://intl.cloud.tencent.com/document/product/267/39604).

![](https://qcloudimg.tencent-cloud.cn/raw/bb10b3c8d970e26d45d55eec229b5fb0.png)
5. **Preview streams**. After completing the above steps, you can enable preview to preview the stream on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/efaa6ffdf3d1dac7ac6d23beac569671.png)
6. Enter a WebRTC push URL or click **Generate** and complete the following configuration:
	- Select your push domain.
	- Enter a unique `AppName` for an application to distinguish it from other applications under the same domain name. `AppName` is `live` by default.
	- Enter a custom `StreamName`, such as `test`.
	- Select an expiration time, such as `2021-08-28 16:16:52`.
	- Click **Confirm**, and a push URL is auto-generated.
![](https://qcloudimg.tencent-cloud.cn/raw/3437d3d4e57ae021aa3e0bea3e6fc4e6.png)
7. Click **Start Push** to start streaming. To enable/disable video or audio, click ![](https://main.qcloudimg.com/raw/da098f4e5ab01021e3c4704b0de41240.png) or (https://main.qcloudimg.com/raw/aa8d8d4c9c32359a249de37ed0d723be.png). After you disable video/audio, data capturing will continue and push will still succeed, but the stream cannot be previewed and will have no video or audio.
>? You cannot enable or disable preview after push succeeds, and you may incur bandwidth/traffic costs or the costs of other value-added services for pushing streams.

![](https://qcloudimg.tencent-cloud.cn/raw/f8e3e7571205090d9ad14a4faa280125.png)
8. After push succeeds, click **View** below the preview to view streaming statistics. You cannot obtain statistics or playback URLs for push URLs not under your account. Please use a push domain under your account to generate push URLs or relay streams to your account.

![](https://qcloudimg.tencent-cloud.cn/raw/5ef686d9d9cb0355a8e4a5686cbcaee3.png)
9. If you have added a playback domain in **Domain Management**, you can **select the domain** to generate a playback URL. To generate a URL of a transcoded stream, you need to bind the playback domain with a transcoding template first.

![](https://qcloudimg.tencent-cloud.cn/raw/94d9969c54c3c0524e1c69f9dbf56d8d.png)
A playback URL is made up of four parts, as shown below:
![](https://main.qcloudimg.com/raw/9094e537a4ae7cecc7feb9c88fb83a55.png)Supported protocols include RTMP, FLV, HLS, and UDP. You can also click the QR code icon and scan the QR code using the [TCToolkit app](https://intl.cloud.tencent.com/document/product/1071/38147) to obtain the playback URL.
![](https://qcloudimg.tencent-cloud.cn/raw/9aa53207e02123a5fa7a4afae1d07724.png)

>! If HTTPS is enabled for the playback domain selected, the FLV and HLS URLs generated will start with https.


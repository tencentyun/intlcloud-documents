VOD provides the superplayer feature free of charge. It allows configuring adaptive bitrate streaming, image sprite, and definition name, so you can use it to specify the output for adaptive bitrate streaming, specify image sprites as thumbnails, and specify the definition name. You can also use it to preview videos in the console.

> ! Superplayer only supports previewing videos processed with adaptive bitrate streaming. If you want to quickly generate videos in compliance with the requirements of the superplayer, please see [Using Superplayer for Playback - Integration Guide](https://intl.cloud.tencent.com/document/product/266/38098).

For videos output by adaptive bitrate streaming, VOD supports previewing them with superplayer in the console.

<span id="sp_set"></span>
## Superplayer Configuration

1. Log in to the VOD console and click **[Superplayer Configuration](https://console.cloud.tencent.com/vod/distribute-play/super-player)** on the left sidebar on the **non-admin** page.
2. Click **Create** to create a superplayer that meets your needs. You can customize three configuration items: **adaptive bitrate streaming for playback**, **image sprite for thumbnail preview**, and **substream for player display**.
<table><tr><th>Configuration Item</th><th>Description</th></tr>
<tr>
<td>Adaptive bitrate streaming for playback</td>
<td>This indicates the adaptive bitstream that this superplayer can play back, which is the adaptive bitstream you customize in <a href="https://intl.cloud.tencent.com/document/product/266/14059">**Template Settings**</a>.</td>
</tr><tr>
<td>Image sprite for thumbnail preview</td>
<td>This indicates the specification of the image sprite that this superplayer can play back, which is the screencapture template you customize in <a href="ttps://intl.cloud.tencent.com/document/product/266/14059">**Template Settings**</a>.</td>
</tr><tr>
<td>Substream for player display</td>
<td>This indicates the name display of the superplayer when it uses different substreams. You can use the default substream name or customize one.</td>
</tr></table>
3. Click **OK**.

<span id="v_pre"></span>
## Superplayer Preview
After creating a superplayer configuration, you can get the **configuration name** of the corresponding superplayer. Go to **Media Assets**, select a video, click **Manage** in the **Operation** column on the right, and select the corresponding configuration name in [Parameter Information](#parameter) to configure and preview different superplayers.

<span id="parameter"></span>
### Parameter information
"Playback Configuration" contains all the playback configurations created in the [superplayer configuration](#sp_set), where `default` and `basicDrmPreset` are the default configurations.
>! Except the `default` playback configuration, all playback configurations can be used only after [key hotlink protection is enabled](https://console.cloud.tencent.com/vod/distribute-play/domain) for the primary distribution domain name.

![](https://main.qcloudimg.com/raw/de33b99efb54a2d4c5b87f5b99eeb2c3.png)

### Configuration item

Configuration items display the configuration content in the selected playback configuration.
- If a `fileID` has an adaptive bitrate streaming name for playback and image sprite for thumbnail preview, it can be directly previewed in the web player and device player.
- If a `fileID` has no adaptive bitrate streaming name for playback or image sprite for thumbnail preview, the following message will be displayed:
![](https://main.qcloudimg.com/raw/51898b5448129952aee19663395e23ee.png)
  This means that the video doesn't meet the video or image sprite specification under this player configuration, and you can use this player configuration only after transcoding the video to the corresponding adaptive bitrate streaming and image sprite specifications.


### Playback control
You can enable key hotlink protection for the playback domain name, so that you can use parameter configuration to control the **Playback URL Validity**, **Preview Duration**, and **Max Playback IPs**:

| Parameter | Description |
| ---------------- | ------------------------------------------------------------ |
| Playback URL Validity | Specifies the expiration time of the video URL |
| Preview Duration | Specifies the preview duration of the video, which must be more than 30 seconds. If this parameter is left empty, there will be no limit on the preview duration |
| Max Playback IPs | Specifies the maximum number of IPs allowed for playback |



## Video Preview
If a `fileID` has an adaptive bitrate streaming name for playback and image sprite for thumbnail preview, it can be directly previewed in the [web player](#web_play) and [device player](#terminal_play).

<span id="web_play"></span>
### Web player
You can click a video to preview it in the web player. You can also click **Copy Code** to embed it into a custom webpage.
![](https://main.qcloudimg.com/raw/2fe7c2de5d56411b37a15b3a0721407d.png)


<span id="terminal_play"></span>
### Device player
1. Scan the QR code below to download the Video Cloud Toolkit app.
   ![](https://main.qcloudimg.com/raw/0f9716d34bac939eb3fc88edb7d0871d.png)
	
	 >? We recommend you use QQ or a browser to scan the QR code and download the demo for Android.
2. Use the Video Cloud Toolkit to scan the QR code or enter the `appID` and `fileID` to preview the video on the terminal device.



   

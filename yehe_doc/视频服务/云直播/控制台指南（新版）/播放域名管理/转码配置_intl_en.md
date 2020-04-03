## Operation Scenarios
Live streaming playback is outputted to the original bitrate by default. If you want to limit or set the playback bitrate, you can do so in the transcoding configuration.
## Prerequisites
You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).

## Directions
1. In **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click **Manage** or the playback domain name to be configured to enter the Domain Management page.
2. In **Template Configuration**, view the **Recording Configuration** tab.
3. Click **Edit** to select a transcoding configuration which specifies the codec and bitrate set by the transcoding template for the playback address under the domain name.
4. Click **Save**.

>> 
>- The template configuration will take effect in about 5–10 minutes.
>- A transcoding configuration template needs to be created in [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31062) first. Once created, it can be selected here.

![](https://main.qcloudimg.com/raw/8ab50571f4260ba070cf3270f8487e30.png)

4. After the transcoding template is configured, the transcoding template name needs to be added to the playback URL. The splicing format is `playback address_transcoding template name`. If it is not added, the original live stream content will be played back.
	> For example, if the original playback address is `http://domain/AppName/StreamName.flv`, and the name of the transcoding template associated with `domain` is `_hd`,
	>Then, if you want to get the output video, the transcoded playback address should be `http://domain/AppName/StreamName_hd.flv`.

>To unbind the transcoding configuration from the domain name, click **Edit** in **Template Configuration**, deselect the corresponding template, and click **Save**.
>![](https://main.qcloudimg.com/raw/8ab50571f4260ba070cf3270f8487e30.png)

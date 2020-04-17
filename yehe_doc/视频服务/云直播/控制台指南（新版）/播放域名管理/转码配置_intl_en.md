## Operation Scenarios
Live streaming playback is outputted to the original bitrate by default. If you want to limit or set the playback bitrate, you can do so in the transcoding configuration.
## Prerequisites
- You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).
- You have created a **transcoding template**. For more information, please see [Transcoding Template Configuration](https://intl.cloud.tencent.com/document/product/267/31071).

## Binding Transcoding Configuration
> The template configuration will take effect in about 5–10 minutes.

1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the playback domain to be configured or **Manage** on its right to enter the domain management page.
2. Select the **Template Configuration** tab, view the **Transcoding Configuration** tab, and click **Edit** on the right.
3. Select a transcoding configuration which specifies the codec and bitrate set by the transcoding template for the playback address under the domain name.
4. Click **Save**.



![](https://main.qcloudimg.com/raw/8ab50571f4260ba070cf3270f8487e30.png)

4. After the transcoding template is configured, the transcoding template name needs to be added to the playback URL. The splicing format is **playback address_transcoding template name**. If it is not added, the original live stream content will be played back.
**For example,** if the name of the transcoding template associated with the playback domain name is **hd**, and the original playback address is:
<pre>
http://domain/AppName/StreamName.flv?txSecret=Md5(key+<b style="color:red;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
Then, if you want to get the output video, the following new playback address needs to be generated:
<pre>
http://domain/AppName/<b style="color:red;">StreamName_hd</b>.flv?txSecret=Md5(key+<b style="color:red;">StreamName_hd</b>+hex(time))&txTime=hex(time)
</pre>
>For more information on playback address, please see [Playback Configuration](https://intl.cloud.tencent.com/document/product/267/31058).

## Unbinding Transcoding Configuration
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the playback domain to be configured or **Manage** on its right to enter the domain management page.
2. Select the **Template Configuration** tab and select **Transcoding Configuration**.
3. Click **Edit** on the right and uncheck the corresponding template.
4. Click **Save** to unbind the template from the domain name.
![](https://main.qcloudimg.com/raw/497478a836b8017c7e8be177b26af24d.png)

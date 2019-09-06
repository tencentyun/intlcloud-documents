## Scenario
LVB outputs playback streams with the original bitrate by default. To limit or set the playback bitrate, please go to transcoding configuration.
## Prerequisites
You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).

## Steps
1. Select **Manage Domain** in the left sidebar, click the playback domain name to be configured or click **Manage** in the operation column to enter the domain name management page.
 ![](https://main.qcloudimg.com/raw/fc654c3ddb6a9e4eda3093e01ca9b8ec.png)

2. In the **Configure Template** tab, you can find information on transcoding configuration of the domain name.
 ![](https://main.qcloudimg.com/raw/5c9ddbc99807cd5733c836554a1fb478.png)

3. By clicking **Edit**, you can select a transcoding configuration to specify the coding format and bitrate set by the transcoding template for the playback address under the domain name.
>A transcoding configuration template needs to be created in [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31071) first. Once created, it can be selected here.

 ![](https://main.qcloudimg.com/raw/8ab50571f4260ba070cf3270f8487e30.png)

4. After you configure the transcoding template, you need to add the transcoding template name to the playback URL. The format is playback address_transcoding template name. Otherwise, you will only be able to play back the original live stream content.
> For example: The original playback address is http://domain/AppName/StreamName.flv, and the name of the transcoding template associated with the domain name is hd.
> If you want to play back transcoded video, you need to use http://domain/AppName/StreamName_hd.flv as your transcoded playback address.

>If you want to unbind the transcoding configuration from the domain name, click **Edit** in **Configure Template**, deselect the corresponding template, and click **Save**.
![](https://main.qcloudimg.com/raw/497478a836b8017c7e8be177b26af24d.png)

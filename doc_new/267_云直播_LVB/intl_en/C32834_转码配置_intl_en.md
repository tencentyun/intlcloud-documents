## Scenario
Live streaming playback is outputted to the original bit rate by default. If you want to limit or set the playback bit rate, you can do so in the transcoding configuration.
## Prerequisites
You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).

## Directions
1. Select **Domain Name Management** in the left sidebar and click **Manage** or the playback domain name to be configured to enter the domain name management page.
 ![](https://main.qcloudimg.com/raw/fc654c3ddb6a9e4eda3093e01ca9b8ec.png)

2. In the **Template Configuration** tab, you can see the transcoding configuration information of the domain name.
 ![](https://main.qcloudimg.com/raw/5c9ddbc99807cd5733c836554a1fb478.png)

3. Click **Edit** to select a transcoding configuration which specifies the coding format and bit rate set by the transcoding template for the playback address under the domain name.
>A transcoding configuration template needs to be created in [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31071) first. Once created, it can be selected here.

 ![](https://main.qcloudimg.com/raw/8ab50571f4260ba070cf3270f8487e30.png)

4. After the transcoding template is configured, the transcoding template name needs to be added to the playback URL. The splicing format is playback address_transcoding template name. If it is not added, the original live stream content will be played back.
> For example: The original playback address is http://domain/AppName/StreamName.flv, and the name of the transcoding template associated with domain is hd.
> If you want to get the video after transcoding, the transcoded playback address should be http://domain/AppName/StreamName_hd.flv
>If you want to unbind the transcoding configuration from the domain name, click **Edit** in **Template Configuration**, deselect the corresponding template, and click **Save**.

![](https://main.qcloudimg.com/raw/497478a836b8017c7e8be177b26af24d.png)

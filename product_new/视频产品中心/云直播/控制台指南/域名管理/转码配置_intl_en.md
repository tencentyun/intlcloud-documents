## Scenario
LVB outputs playback streams with the original bitrate by default. To limit or set the playback bitrate, please go to transcoding configuration.
## Prerequisites
You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).

## Steps
1. Select **Manage Domain** in the left sidebar, click the playback domain name to be configured or click **Manage** in the operation column to enter the domain name management page.
 ![](https://main.qcloudimg.com/raw/1915b8c56c476154a94da28fe95f6141.png)

2. In the **Configure Template** tab, you can find information on transcoding configuration of the domain name.
 ![](https://main.qcloudimg.com/raw/6779c732fd9f2dd96cfd97a5b3ac4059.png)

3. By clicking **Edit**, you can select a transcoding configuration to specify the coding format and bitrate set by the transcoding template for the playback address under the domain name.
>! A transcoding configuration template needs to be created in [Transcoding Configuration](https://cloud.tencent.com/document/product/267/20385) first. Once created, it can be selected here.

 ![](https://main.qcloudimg.com/raw/f1ee992eb425c995e49fe839bf5d0b7a.png)

4. After you configure the transcoding template, you need to add the transcoding template name to the playback URL. The format is playback address_transcoding template name. Otherwise, you will only be able to play back the original live stream content.
> For example: The original playback address is http://domain/AppName/StreamName.flv, and the name of the transcoding template associated with the domain name is hd.
> If you want to play back transcoded video, you need to use http://domain/AppName/StreamName_hd.flv as your transcoded playback address.

>? If you want to unbind the transcoding configuration from the domain name, click **Edit** in **Configure Template**, deselect the corresponding template, and click **Save**.
>![](https://main.qcloudimg.com/raw/ac484c9593f3e8e80edfc11b2e31b3a9.png)

StreamLive allows you to record live streams for a specified time period. This feature must be used together with Tencent Cloud COS.

Follow the steps below to configure scheduled recording:

1. Go to the COS console to configure the storage of recording files. You can either create a bucket or select an existing bucket. Make sure that the bucket is in the same region as your StreamLive channel. For example, if your StreamLive channel is in Mumbai, then the bucket must also be in Mumbai.
![](https://qcloudimg.tencent-cloud.cn/raw/15154bc8dfecc79a6d59a913cbd0741a.png)

2. Click the bucket name to go to the configuration page and select **File List** on the left sidebar. Click **Create Folder** to create a folder for the recording files.
![](https://qcloudimg.tencent-cloud.cn/raw/077dfa198a68ac0f77bc6716e65c41a7.png)

3. Enter a folder name and splice it to the endpoint URL of the bucket. The result is the address where StreamLive recording files will be saved.
![](https://qcloudimg.tencent-cloud.cn/raw/474ebe6587dec1f4172d94226f8fc142.png)

You can view the endpoint URL of a bucket on the **Overview** page.
![](https://qcloudimg.tencent-cloud.cn/raw/3133262319ef5735ae287ef2821a5af0.png)

In the example above, the address to save StreamLive recording files is `https://${your-bucket-name}-${appid}.cos.ap-mumbai.myqcloud.com/streamlive-scheduled-record`. Note it for later use.

4. Go to the StreamLive console. Click the name of the channel for which you want to configure scheduled recording and select the **Plan** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/e87cbf8e8ff1042941c99c5c946b4dc1.png)

5. Click **Create Event** and complete the following settings.
![](https://qcloudimg.tencent-cloud.cn/raw/2ae655ad72824ca958a87fe1461d5ba2.png)
- **Event Type**: Select **Time Record**.
- **Event Name**: Enter a name for the recording event.
- **OutputGroupName**: Select from the drop-down list an output group added to the channel.
- **ManifestName**: The name of the playlist file. For HLS outputs, the file format is M3U8. For DASH outputs, the file format is MPD.
- **DestinationUrl1**: Enter the full COS path (including the bucket name) to save the recording files.
- **Timing**: Specify the time period to record the stream.

6. Click **Confirm**. This concludes the configuration. The channel will record the stream it receives during the specified time period and save the recording files to the specified destination.



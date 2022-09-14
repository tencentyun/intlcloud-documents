StreamLive allows you to save HLS/DASH streams to Tencent Cloud COS.

On the **Output Group Setting** page, select HLS_ARCHIVE or DASH_ARCHIVE as the **Output Group Type** and enter the COS address to save streams in **COS Destination**. After the channel is started, the live stream will be archived to COS in real time.
![](https://qcloudimg.tencent-cloud.cn/raw/2d18dc7f0100da76ffc40df26ea7e158.png)

The difference between archiving and relay is that with archiving, the manifest file includes all audio/video files of the channel from the start to the end, but with relay, the manifest file is updated constantly and only includes the latest audio/video files.

The formats of the main manifest file for HLS and DASH streams are as follows:
- HLS: ${COS Destination}/${region}/${ChannelId}-${p0 or p1}/${OutputGroupName}/${OutputGroupName}.m3u8
- DASH: ${COS Destination}/${region}/${ChannelId}-${p0 or p1}/${OutputGroupName}/${OutputGroupName}.mpd




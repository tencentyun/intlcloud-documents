StreamLive allows you to push HLS/DASH streams to an HTTP server using the HTTP PUT method.

On the **Output Group Setting** page, select HLS or DASH as the **Output Group Type** and enter the address of the HTTP server in **Destination**. After the channel is started, the live stream will be pushed to the destination URL in real time.
![](https://qcloudimg.tencent-cloud.cn/raw/f03e405e1b2ebd07285e28e6b5fd1f49.png)

The difference between archiving and relay is that with archiving, the manifest file includes all audio/video files of the channel from the start to the end, but with relay, the manifest file is updated constantly and only includes the latest audio/video files.

The format of the manifest file for HLS and DASH streams is as follows:
- HLS: ${Destination}/${OutputGroupName}.m3u8
- DASH: ${Destination}/${OutputGroupName}.mpd

Relay also supports HTTP authentication. To enable it, toggle on **Authentication** in the **Destination** area and enter the authentication information.

StreamLive支持将HLS/DASH归档到腾讯云COS。

设置方式为在**Channel**的**Output Group Setting**中，需要将**Output Group Type**选择为HLS_ARCHIVE/DASH_ARCHIVE，并在**COS Destination**中填写包含存储路径的COS URL地址。在Channel运行期间，直播文件将会实时归档到COS中。
![](https://qcloudimg.tencent-cloud.cn/raw/2d18dc7f0100da76ffc40df26ea7e158.png)

归档和直播转推的区别为：归档时Manifest文件内容是包含从频道启动到结束时所有的音视频文件列表，而直播转推中Manifest文件内容会实时更新，只包含最新部分的音视频文件列表。

HLS和DASH的主Manifest文件格式为：
- HLS：${COS Destination}/${region}/${ChannelId}-${p0 or p1}/${OutputGroupName}/${OutputGroupName}.m3u8
- DASH：${COS Destination}/${region}/${ChannelId}-${p0 or p1}/${OutputGroupName}/${OutputGroupName}.mpd




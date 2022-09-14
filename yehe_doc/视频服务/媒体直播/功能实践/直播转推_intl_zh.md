StreamLive支持通过HTTP PUT的方式，输出直播流（HLS/DASH）到HTTP服务器。

设置方式为在Channel的**Output Group Setting**中，将**Output Group Type**选择为HLS/DASH，并在**Destination**中填写推送目标URL路径。在Channel运行期间，直播文件将会实时推送到目标URL中。
![](https://qcloudimg.tencent-cloud.cn/raw/f03e405e1b2ebd07285e28e6b5fd1f49.png)

归档和直播转推的区别为：归档时Manifest文件内容是包含从频道启动到结束时所有的音视频文件列表，而直播转推中Manifest文件内容会实时更新，只包含最新部分的音视频文件列表。

HLS和DASH转推的主Manifest文件格式为：
- HLS：${Destination}/${OutputGroupName}.m3u8
- DASH：${Destination}/${OutputGroupName}.mpd

推送还支持HTTP鉴权，在Destination中开启**Authentication**，并填写相关鉴权信息即可。

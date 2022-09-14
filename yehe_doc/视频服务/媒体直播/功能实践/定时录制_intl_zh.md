StreamLive 支持对频道直播流进行定时录制，需要搭配云存储 COS 产品一起配合使用。

配置步骤如下：

1. 首先进入云存储COS控制台，进行录制目标存储地址的配置，这里您可以选择已有存储桶，也可以新建存储桶，但需要注意所属区域一定要和 StreamLive频道保持一致，例如：如果StreamLive 频道配置在孟买，则录制目标存储桶也需要在孟买。
![](https://qcloudimg.tencent-cloud.cn/raw/15154bc8dfecc79a6d59a913cbd0741a.png)

2. 点击存储桶名称进入配置界面，进入**文件列表**页，点击**创建文件夹**，为StreamLive 录制功能创建目标路径，便于集中管理录制文件。
![](https://qcloudimg.tencent-cloud.cn/raw/077dfa198a68ac0f77bc6716e65c41a7.png)

3. 为该路径命名，并与所属存储桶的访问域名拼接后构成StreamLive定时录制文件目标推送地址。
![](https://qcloudimg.tencent-cloud.cn/raw/474ebe6587dec1f4172d94226f8fc142.png)

所属存储桶的**访问域名**，可以在存储桶**概览页**的**域名信息**框中查询。
![](https://qcloudimg.tencent-cloud.cn/raw/3133262319ef5735ae287ef2821a5af0.png)

如上图的例子中所示，StreamLive 定时录制文件目标推送地址为https://${your-bucket-name}-${appid}.cos.ap-mumbai.myqcloud.com/streamlive-scheduled-record，提前记录下该地址以备后续配置时使用。

4. 回到StreamLive频道配置页面，点击需要进行定时录制的频道名称，进入**Plan**标签页进行配置。
![](https://qcloudimg.tencent-cloud.cn/raw/e87cbf8e8ff1042941c99c5c946b4dc1.png)

5. 点击**Create Event**，在对话框中填入相关配置信息。
![](https://qcloudimg.tencent-cloud.cn/raw/2ae655ad72824ca958a87fe1461d5ba2.png)
- **Event Type**：选择 Time Record。
- **Event Name**：为本次录制事件进行自定义命名。
- **OutputGroupName**：下拉菜单选择本频道已配置的输出组名称。
- **ManifestName**：录制文件播放列表文件名称。若频道输出格式为HLS，则该文件列表后缀名为m3u8，若为DASH格式，则后缀名为mpd。
- **DestinationUrl1**：输入之前已创建好并记录下来的完整COS存储路径，包含存储桶域名。
- **Timing**：选择需要进行录制的时间段信息。

6. 点击**Confirm**确认提交后便可完成定时录制配置。频道在收到推流信号后，会按照已配置时间段进行视频录制并将文件推送至预设目标地址。



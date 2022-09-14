在本节中，将为您介绍如何配置StreamPackage。

1. 进入[StreamPackage控制台首页](https://console.tencentcloud.com/mdp/channel)，首先按照您的业务需求选择就近区域：![](https://qcloudimg.tencent-cloud.cn/raw/9e2a246d5681ee392a1c8c70cd342de3.png)
2. 点击**Create Channel**创建频道，输入配置必要信息：![](https://qcloudimg.tencent-cloud.cn/raw/beef79acbc0bb01fdc795adabd23cf83.png)
- **Input Protocol**： 可支持 HLS 以及 DASH，此处以HLS为例。
- **Max Segment Duration**：表示向本频道推送HLS流的ts文件的最大时长，建议配置为4秒。
- **Max Playlist Duration**：表示向本频道推送HLS流的m3u8播放列表文件的最大时长，建议配置为12秒，即m3u8中包含3个分片。

3. 提交必要配置信息后，会自动进入频道高级配置页面。**Information**中会展示配置信息，并且可针对其中的直播推送地址**Input**、回源拉流地址**Endpoints**以及**CDN** 加速进行进一步配置。

4. **Input**：系统会自动创建两个Input推送节点地址，以便于您进行主备推送操作从而实现高可用直播源站服务。
![](https://qcloudimg.tencent-cloud.cn/raw/48526b3405cd4373f41f95aa254c4a37.png)
- 其中对于每一路 Input 均支持配置独立的访问认证信息，当您打开**Input Authentication** 开关后，系统会自动创建一组**Username / Password**。此处插入![](https://qcloudimg.tencent-cloud.cn/raw/c32de384eda1fa084d50b13f243a9021.png)
- 此时若点击**Rotate credentials**，则会立即生成一组新的认证信息，原有信息无法恢复。
- 如您需要通过其他第三方服务向该地址推送直播流数据，请提前记录下**Input Url**以及**Authentication**信息。

5. **Endpoint**：进入**Endpoint**标签页，点击**Create Endpoint** 以创建回源拉流节点地址，这里支持两种访问控制方式：IP黑白名单（IP Restriction）、鉴权秘钥（AuthKey）。由于创建Channel时选择了HLS协议，故系统也会生成一个HLS的回源地址，该地址实际为main.m3u8的完整路径。
![](https://qcloudimg.tencent-cloud.cn/raw/43f73db0ecaba6c72d7eb4677397caad.png)

6. 至此，StreamPackage频道配置已完成，回到**Channel Management**首页，在频道列表中找到刚才配置的频道，并记录下频道**ID** 以及**Endpoint Url**，以备后续操作配置时使用。
![](https://qcloudimg.tencent-cloud.cn/raw/5eb1b481f758f89ec7a1279d7bd4d873.png)
![](https://qcloudimg.tencent-cloud.cn/raw/3f7c30d33e17425a44dca05a701e8ad7.png)
本文以OBS、VLC作为推流及播放工具为例，在OBS的推流配置中填入 StreamLive 的 Input 推流地址，第一行服务器填入推流域名+应用名，第二行串流密钥填入流名称，如下图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/d19308151baf27053d3ef774f416274c.png)

打开 VLC，在 File 菜单选择 Open Network，填入网络直播串流地址，这里将刚才提前记录的StreamPackage的Endpoint地址填入，并将其中的域名替换为CSS中已配置的播放域名，即可进行播放。
![](https://qcloudimg.tencent-cloud.cn/raw/e5d6e5f9c304f6b38fffafca19c0b456.png)

至此由StreamLive+StreamPackage+CSS共同构建的高可靠性云直播平台已可正常稳定工作。
![](https://qcloudimg.tencent-cloud.cn/raw/3096992f56506043045b681624e12770.png)
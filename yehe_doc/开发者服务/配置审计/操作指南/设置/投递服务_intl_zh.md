### 投递资源时间线

点击**设置-投递服务**菜单，进入**投递服务**页面，点击**开启**即可创建投递服务，将资源时间线中的定时配置历史记录投递至您指定的 COS 存储桶，以便于您对资源配置数据执行更为精细化的分析、以及更长时间的存储。
![](https://qcloudimg.tencent-cloud.cn/raw/85f4b40754ca9e992eacc3fa63d60afb.png)
![](https://qcloudimg.tencent-cloud.cn/raw/b3347143ed82a4bc21b779b49bb1b0bc.png)
对于开启投递服务后，当时间线更新时，配置审计每日00:30将向您指定的 COS 存储桶投递资源配置变更历史。当您**关闭**投递服务，时间线的更新不会存储到对应的存储桶。
![](https://qcloudimg.tencent-cloud.cn/raw/753fdf6ae5d0bb7dc596036ebda49e7f.png)
![](https://qcloudimg.tencent-cloud.cn/raw/570f9d8479e7224f7400cb0a2f50a23c.png)
因数据量较大，资源配置快照拉取及投递到 COS 存储桶有15分钟的窗口期，导致投递至 COS 存储桶的数据更新存在一定延时，请耐心等待。


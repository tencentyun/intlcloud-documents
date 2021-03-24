## 操作场景

如果您有自建源站和直播源内容，并且需要通过腾讯云进行直播播放；或者已经接入MediaPackage ，希望通过直播CDN分发直播流，可以通过云直播源站配置功能回源拉取直播内容。配置成功后，您可通过云直播回源自有源站/MediaPackage 进行直播拉流和内容分发。本文档将指导您如何设置源站信息。

## 注意事项

-  配置好相关信息后，源站设置会在**30分钟**-**1个小时**左右生效。
-  开启源站配置功能后，该播放域名的不支持通过 StreamName 匹配其他推流域名进行拉流，而且该域名无法使用水印、转码、录制、截图、鉴黄等功能。 

## 前提条件

- 已登录 [云直播控制台](https://console.cloud.tencent.com/live)。
- 已搭建直播源站，或已在MediaPackage创建频道。
- 已添加**播放域名**。

## 操作步骤

1. 进入[【域名管理】](https://console.cloud.tencent.com/live/domainmanage)，单击需配置的**播放域名**或右侧的【管理】进入域名详情页。
2. 选择【高级配置】，查看【源站设置】标签。
3.  单击源站设置模块的【编辑】，打开【源站设置】滑动开关，选择【源站类型】开始设置源站信息：
 - **选择的源站类型为【直播源站】**：
		1. 选择【回源协议】，勾选【播放协议】。
		2. 选择【源站地址ip/domain】，支持选择 IP 地址或选择域名两种模式。
		3. 根据选择的ip地址或域名，输入对应的【主源地址】。
        ![](https://main.qcloudimg.com/raw/5e085f15c5cd0d09282774f40231301c.png)
  >?**回源协议**指云直播回源拉流时支持的格式。**播放协议**指直播内容通过直播 CDN 分发时的播放协议。
  >
  >- 回源协议为 FLV/RTMP 时，播放协议支持 FLV/HLS。
  >- 回源协议为 HLS 时，播放协议只支持 HLS。
  >- 回源协议不支持多选，播放协议支持多选。

   - **选择的源站类型为【MediaPackage】**：
     1. 若未授权MediaPackage访问LVB，点击【服务授权】进行授权操作。
     ![](https://main.qcloudimg.com/raw/43f726d167d7d5d1881fbb6902ee5660.png)
     2. 使用MediaPackage功能，需授权允许访问MediaPackage资源，点击【前往授权】，跳转至【角色管理】创建服务预设角色并授予MediaPackage相关权限。
     ![](https://main.qcloudimg.com/raw/a29b66065ef5c2af5bccc7c00be76404.png)
     3. 点击【同意授权】，完成授权MediaPackage访问LVB。
     ![](https://main.qcloudimg.com/raw/8cd1d5175c0852fc6d96c52bbf185190.png)
     4. 同意授权后，跳回源站设置页面，点击【已完成授权】。
     ![](https://main.qcloudimg.com/raw/baaa2d4a8958b19cc33d1597d2440051.png)
     5. 完成服务授权后，若MediaPackage无地区频道，[选择地区并创建频道](https://console.cloud.tencent.com/mdp/channel)，输入频道名，选择输入协议（支持HLS/DASH），填写HLS/DASH协议的相关参数，点击【创建】保存频道配置，再继续源站配置。
     ![](https://main.qcloudimg.com/raw/ebbcc77e970a6bd8b27421e3c84b6858.png)
		 ![](https://main.qcloudimg.com/raw/b4f1e27fa02c93b88a47a1de9a583ee9.png)
     6. 创建频道后，即可在源站设置里选择MediaPackage【地区】和【频道】。
        ![](https://main.qcloudimg.com/raw/1cfce64cba34b65c9293a6f40d2109cd.png)
     >?
     >- 回源协议为 DASH / HLS 时，需要向CDN发布配置支持，需开发提供 DASH、HLS 配置文件的模板，客户在控制台选择 MediaPackage 保存后，默认向 CDN 发送配置。
     >- MediaPackage删除频道后，由于没有删除绑定关系，故这边仍会正常显示绑定关系，但是无法正常回源。
     >- 地区不支持多选，但可选择该地区下多个频道，回源协议和播放协议跟随频道，无需用户选择。

4. 单击【保存】即可保存配置。

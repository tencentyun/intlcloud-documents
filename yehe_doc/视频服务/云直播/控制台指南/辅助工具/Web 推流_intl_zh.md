## 操作场景
腾讯云为您提供 Web 推流功能，可实现快速生成推流地址，在线推流测试直播功能。

## 前提条件
- 已登录 [云直播控制台](https://console.cloud.tencent.com/live)。
- 已添加 [推流域名](https://intl.cloud.tencent.com/document/product/267/35970)。
- 您的设备已安装摄像头，并浏览器支持 Flash 插件调用摄像头权限。

## 操作步骤
1. 登录云直播控制台，选择[【Web推流】](https://console.cloud.tencent.com/live/tools/webpush)。
2. 在 Web 端推流的页面进行以下设置：
	- 选择推流域名。
	- 填写自定义的流名称 StreamName，例如：`test`。
	- 选择过期时间，例如：`2020-04-13 23:59:59`。
	- 编辑 AppName，用于区分同一个域名下多个 App 的地址路径，默认值为 live。
3. 单击【开始推流】，授权允许调用摄像头，即可开始推流。
![](https://main.qcloudimg.com/raw/1d9741fe544d1c850ab89b22134f6dc8.png)
4. 若您在【域名管理】中已添加播放域名，即可在下方查看对应生成的播放地址。其中，播放地址由以下4部分组成：
![](https://main.qcloudimg.com/raw/9094e537a4ae7cecc7feb9c88fb83a55.png)
支持 RTMP、FLV 和 HLS 协议，可以单击播放地址后的二维码，通过 精简版 Demo 扫码查看播放地址：
![](https://main.qcloudimg.com/raw/d91fe5d373cfc03df2c87562f3984858.png)

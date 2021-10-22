本文档将指导您快速将本地视频上传至云点播，并使用云点播服务处理该视频，最终实现**在 Web 页面可直接观看经过加速后且含水印的转码视频**。以本地视频文件“腾讯云.mp4”为例。


## 步骤1：开通云点播
1. 注册 [腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985)，并完成 [实名认证](https://intl.cloud.tencent.com/document/product/378/3629)。
2. 购买云点播服务，具体请参见 [计费概述](https://intl.cloud.tencent.com/document/product/266/2838)。
3. 选择【云产品】>【视频服务】>[【云点播】](https://console.cloud.tencent.com/vod)，进入云点播控制台。

>?若已开通云点播服务，请直接进入下一步骤。



## 步骤2：上传视频
1. 单击左侧导航栏的[【媒资管理】](https://console.cloud.tencent.com/vod/media)。
2. 单击【上传视频】，【上传方式】配置项选择【本地上传】。
![](https://main.qcloudimg.com/raw/1d54bda88e541f56d8c2fdec162761f0.png)
3. 单击【选择视频】，选择本地视频文件“腾讯云.mp4”。
4. 在【视频处理】配置项选择【只上传，暂不进行视频处理】，最后单击左下角的【开始上传】。

## 步骤3：创建水印模板
1. 在左侧导航栏选择【视频处理设置】>[【模板设置】](https://console.cloud.tencent.com/vod/video-process/template)。
2. 在页签栏选择【水印模板】。
3. 单击【创建水印模板】，在该页面进行如下设置，最后单击【创建】。<br>
<img src="https://main.qcloudimg.com/raw/423f29236a2e12bb8546682db5eb97fc.png" width="450">

## 步骤4：处理视频
1. 在 [媒资管理](https://console.cloud.tencent.com/vod/media) 页签栏选择【已上传】。
2. 选中“腾讯云.mp4”前的勾选框，单击【视频处理】。
![](https://main.qcloudimg.com/raw/246099e6f6c37bca0f3b4901b4125412.png)
3. 在“视频处理”弹框中，【处理类型】配置项选择【转码】。
4. 在【转码模板】配置项，单击【转码模板】，然后选择对应模板（可勾选多个转码模板）。
5. 在【水印模板】配置项，单击下拉框选择【选择水印模板】，右侧弹出下拉框，选择【p001】。
6. 在【视频封面】配置项，勾选即可，最后单击【确定】。
![](https://main.qcloudimg.com/raw/31ecab7ef88cc80f103a16a7dee3deb8.png)

## 步骤5：获取播放链接
1. 单击“腾讯云.mp4”所在行操作栏的【管理】。
2. 单击【标准转码列表】模块中【MP4-标清-SD】对应操作栏下的【复制地址】。
<img src="https://main.qcloudimg.com/raw/18a5e92a1200dfcd67dc5d5d0567159c.png" width="1100">
3. 在 Web 浏览器 URL 地址栏输入已复制的 URL 地址，按下回车键，即可播放该视频。

## 相关操作
- [最佳实践 - 如何通过 Web 上传视频](https://intl.cloud.tencent.com/document/product/266/39106)
- [最佳实践 - 如何对视频进行转码](https://intl.cloud.tencent.com/document/product/266/37546)
- [最佳实践 - 如何使用 Key 防盗链](https://intl.cloud.tencent.com/document/product/266/37544)
- [最佳实践 - 如何接收事件通知](https://intl.cloud.tencent.com/document/product/266/37542)



## 常见问题

- [云点播计费方式如何更改？](https://intl.cloud.tencent.com/document/product/266/18941)
- [云点播支持上传哪些格式的媒体文件？](https://intl.cloud.tencent.com/document/product/266/2846)
- [云点播上传文件有哪些方式，能否断点续传？](https://intl.cloud.tencent.com/document/product/266/2846)


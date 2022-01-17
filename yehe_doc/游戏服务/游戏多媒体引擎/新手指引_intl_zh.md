本文将为刚入门游戏多媒体引擎（GME）的用户提供一条学习的路径。

## 1. 熟悉游戏多媒体引擎

- [游戏多媒体引擎提供了什么样的服务？](https://intl.cloud.tencent.com/document/product/607/10835)
- [游戏多媒体引擎有什么优势？](https://intl.cloud.tencent.com/document/product/607/10837)
- [游戏多媒体引擎的各个应用场景介绍。](https://intl.cloud.tencent.com/document/product/607/10838)
- [语音中常用的概念。](https://intl.cloud.tencent.com/document/product/607/30259)

## 2. 游戏多媒体引擎的计费模式

游戏多媒体引擎目前有多个服务，例如实时语音服务、语音转文本服务以及语音分析服务等，具体计费情况详情请参见 [日结后付费模式](https://intl.cloud.tencent.com/document/product/607/36276)。

## 3. 体验服务

在使用游戏多媒体引擎之前，您可以体验腾讯云的产品服务，直接从 [Demo 体验文档](https://intl.cloud.tencent.com/document/product/607/38535) 扫码下载移动端的程序，或者下载 Windows 平台可执行程序体验 3D 语音效果。

## 4. 新手入门

#### 4.1 开通服务

在使用腾讯云游戏多媒体引擎之前，您需要 [注册腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985) 并且开通游戏多媒体引擎服务。详情请参见 [语音服务配置指引](https://intl.cloud.tencent.com/document/product/607/39698)。

#### 4.2 获取接入参数

使用游戏多媒体引擎开通服务之后，在创建的应用详情页面可以获取到对应的 AppID 和权限密钥。
- 在使用 Demo 时，需要 AppID 以及权限密钥作为参数填入 Demo 中。
- 在使用 SDK 时，初始化接口 Init 需要使用 AppID 作为参数，在鉴权接口 QAVAuthBuffer.GenAuthBuffer（实时语音服务）、ApplyPTTAuthbuffer（语音转文字服务） 均需要权限密钥作为参数。

![](https://main.qcloudimg.com/raw/a63f14a7092169c8c9b54cfd21ce4c12.png)
#### 4.3 下载 SDK

可以通过 [下载指引](https://intl.cloud.tencent.com/document/product/607/18521) 下载所需平台的 SDK 文件。**目前游戏多媒体引擎支持 Windows、Mac、Android 以及 iOS 平台，游戏引擎支持 UnrealEngine4、Unity3D 以及 Cocos2DX**。

目前也支持在 H5 端进行实时语音通话，以及在小程序端听房间内的语音聊天。

#### 4.4 接入 SDK
接入各平台 SDK 可以先参考各平台的 [工程配置](https://intl.cloud.tencent.com/document/product/607/10783) 文档，配置工程完成后再查看对应平台的 [接口文档](https://intl.cloud.tencent.com/document/product/607/15228) 调用接口使用游戏多媒体引擎服务。实时语音服务接口的调用顺序一般是【Init 初始化】>【Poll 触发回调】>【EnterRoom 进入语音房间】>【EnableMic 打开麦克风】>【EnableSpeaker 打开扬声器】>【ExitRoom 退房】>【Unit 反初始化】。

**实时语音服务进房流程如下所示：**
<img src="https://main.qcloudimg.com/raw/d23fd88b9d0ff2f044f7549168be9d79.png"  width="60%" /></img>

## 5. 控制台运营指引
有关实时语音、语音消息以及语音分析的后台数据，详情可参见 [运营指引](https://intl.cloud.tencent.com/document/product/607/17448)。

## 6. 文档功能概述

<table>
<thead>
<tr>
<th>如果您想</th>
<th>您可以阅读</th>
</tr>
</thead>
<tbody><tr>
<td>下载 SDK 文件。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18521" target="_blank">下载指引</a></td>
</tr>
<tr>
<td>扫码下载应用，体验游戏多媒体引擎服务。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/38535" target="_blank">Demo 体验文档</a></td>
</tr>
<tr>
<td>将 SDK 接入工程中，以及查阅 SDK 导出工程时候所需要的配置。（以 Unity 平台为例）</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/10783" target="_blank">Unity 工程配置</a></td>
</tr>
<tr>
<td>将 SDK 接入工程中，查阅全部的接口，实现实时语音服务、语音转文本服务。（以 Unity 平台为例）</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/15228" target="_blank">Unity 接口文档</a></td>
</tr>
<tr>
<td>将 SDK 接入工程中，快速进行实时语音服务接入。（以 Unity 平台为例）</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18248" target="_blank">Unity 快速入门</a></td>
</tr>
<tr>
<td>在实时语音服务中实现范围语音效果（类似吃鸡游戏全局、小队语音效果）。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/17972" target="_blank">范围语音</a></td>
</tr>
<tr>
<td>在游戏中实现 3D 实时说话声音效果。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18218" target="_blank">3D 音效</a></td>
</tr>
<tr>
<td>利用 GME 在实时语音房间里面播放伴奏。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/31504" target="_blank">实时语音伴奏</a></td>
</tr>
<tr>
<td>了解实时语音服务中不同房间类型的区别。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18522" target="_blank">音质选择</a></td>
</tr>
<tr>
<td>进一步了解鉴权的细节以及后台部署方案。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/12218" target="_blank">鉴权密钥</a></td>
</tr>
<tr>
<td>对使用 SDK 时候的错误码进行分析及查询解决方案。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/33223" target="_blank">错误码</a></td>
</tr>
<tr>
<td>了解有关游戏多媒体引擎的产品问题。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30254" target="_blank">一般性问题</a></td>
</tr>
<tr>
<td>在购买服务之前查看计费的规则细节。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30255" target="_blank">计费相关问题</a></td>
</tr>
<tr>
<td>对实时语音服务使用过程中，有关语音房间相关问题的解决方案。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/35611" target="_blank">实时语音进房失败问题</a></td>
</tr>
<tr>
<td>寻求使用 SDK 过程中音频方面问题的解决方案。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/30257" target="_blank">实时语音无声及音频问题</a></td>
</tr>
</tbody></table>


## 7. 新手常见问题
#### 咨询服务问题
[使用游戏多媒体引擎实时语音，流量消耗是多少？](https://intl.cloud.tencent.com/document/product/607/39519)
[GME 有哪些功能？](https://intl.cloud.tencent.com/document/product/607/39520)


#### Demo相关问题
[GME 可以只使用一个 OpenId 吗？](https://intl.cloud.tencent.com/document/product/607/30256)
[如何使用已下载的 Demo？](https://intl.cloud.tencent.com/document/product/607/30256)
[如何取得日志？](https://intl.cloud.tencent.com/document/product/607/39521)
[集成 GME SDK 并导出 Apk 后，启动程序发生黑屏现象，如何解决？](https://intl.cloud.tencent.com/document/product/607/39522)
[在 Xcode 导出可执行文件时，已添加 GMESDK.framework 库，编译时出现编译报错，如何解决？](https://intl.cloud.tencent.com/document/product/607/39522)


#### 实时语音服务相关问题
[GME SDK 中的 poll 函数应何时开始调用？](https://intl.cloud.tencent.com/document/product/607/30254)
[GME 的实时语音房间数量和人数有限制吗？](https://intl.cloud.tencent.com/document/product/607/35611)
[调用 EnterRoom 接口返回值为0，为什么还是没办法进房？](https://intl.cloud.tencent.com/document/product/607/39523)
[出现网络问题，该如何排查？](https://intl.cloud.tencent.com/document/product/607/39519)
[用户在实时语音房间内，但是客户端断网了，将有什么策略？](https://intl.cloud.tencent.com/document/product/607/35611)
[使用实时语音范围语音功能，能正常使用范围语音，但是没有衰减效果，我设置了3D音效文件，返回值也是0。](https://intl.cloud.tencent.com/document/product/607/39523)
[进房后，手机音量变得特别小，开启麦克风后音量又变得很大，怎么解决？](https://intl.cloud.tencent.com/document/product/607/39524)
[Android 手机打开麦克风后，声音从听筒而不是扬声器出来，该如何解决？](https://intl.cloud.tencent.com/document/product/607/30257)

## 8. 反馈与建议
使用腾讯云游戏多媒体引擎产品和服务中有任何问题或建议，您可以通过以下渠道反馈，将有专人跟进解决您的问题：
- 如果发现产品文档的问题，如链接、内容、API 错误等，您可以单击文档页右侧 【文档反馈】或选中存在问题的内容进行反馈。
- 如果遇到产品相关问题，您可 [提交工单](https://console.cloud.tencent.com/workorder/category) 寻求帮助。

>? 提交工单寻求帮助时，请提供 SDK 的版本，以及所使用的平台。

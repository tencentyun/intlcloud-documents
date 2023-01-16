本文将为刚入门游戏多媒体引擎（GME）的用户提供一条学习的路径。
## 1. 熟悉游戏多媒体引擎
- [游戏多媒体引擎提供了什么服务？主要功能是什么？](https://intl.cloud.tencent.com/document/product/607/10835)
- [游戏多媒体引擎有什么优势？](https://intl.cloud.tencent.com/document/product/607/10837)
- [游戏多媒体引擎可以应用在哪些场景？](https://www.tencentcloud.com/zh/document/product/607/51558)

## 2. 游戏多媒体引擎的计费模式
游戏多媒体引擎目前有多个服务，例如实时语音服务、语音消息服务等，具体计费情况详情请参见 [购买指南](https://intl.cloud.tencent.com/document/product/607/50009)。

## 3. 体验服务
在使用游戏多媒体引擎之前，您可以先体验产品效果:

<img src="https://gme-public-1256590279.cos.ap-nanjing.myqcloud.com/GMEResource/IMB_KuI8ov.gif"    width="37.5%"/></img>


- [基本功能体验 Demo](https://intl.cloud.tencent.com/document/product/607/50219)：体验功能包括实时语音、语音消息、转文本、实时语音3D音效、实时语音基础变声功能
- [3D实时语音体验 Demo](https://intl.cloud.tencent.com/document/product/607/50220)：体验实时语音3D音效功能
- [高级变声功能体验 Demo](https://intl.cloud.tencent.com/document/product/607/50221)：体验实时语音高级变声功能


## 4. 开通服务
- 在使用腾讯云游戏多媒体引擎之前，您需要 [注册腾讯云账号](https://intl.cloud.tencent.com/document/product/378/17985) 。
- 在 [腾讯云游戏多媒体控制台](https://console.cloud.tencent.com/gamegme) 开通服务，可根据所需要使用的功能，开通相应的功能服务。详情请参见 [服务开通](https://intl.cloud.tencent.com/document/product/607/10782)。

## 5. 获取接入参数

### 客户端接入参数


1. 在 [腾讯云游戏多媒体控制台](https://console.cloud.tencent.com/gamegme) 中，找到您刚刚创建的应用，在**操作**列单击**设置**，进入应用设置页面

2. 在页面中可以获取到对应的 AppID 和权限密钥。所需参数在控制台的位置截图如下：

	- 在使用 Sample Project 时，需要 AppID 以及权限密钥作为参数填入 Sample Project 中。
	- 在使用 SDK 时，初始化接口 Init 需要使用 AppID 作为参数，在本地鉴权生成接口 QAVAuthBuffer.GenAuthBuffer 中需要权限密钥作为参数传入。

### 云 API 接入参数
如果您使用的是云 API，则需要 SecretId 及 SecretKey，请在 [API 密钥管理](https://console.cloud.tencent.com/cam/capi) 页面获取，建议参考 [安全最佳实践](https://www.tencentcloud.com/document/product/598/10592) 对账号进行访问管理。



## 6. 跑通 Sample Project
GME 各个平台均提供了 SDK 以及 Sample Project。通过跑通 SampleProject，可以协助开发者了解 GME SDK 如何接入。
### 6.1 下载 Sample Project
可以通过 [下载指引](https://intl.cloud.tencent.com/document/product/607/18521) 下载所需平台的 Sample Project。


### 6.2 跑通 Sample Project
根据所使用的平台，查看相应的文档：
[快速跑通 UnrealEngine Sample Project](https://intl.cloud.tencent.com/document/product/607/46014)

## 7. 接入基础功能
### 7.1 下载 SDK
可以通过 [下载指引](https://intl.cloud.tencent.com/document/product/607/18521) 下载所需平台的 SDK 文件。
<img src="https://qcloudimg.tencent-cloud.cn/raw/b04f51788ab7bd527ef1662c5c5f7675.png"  width="50%"/></img>

### 7.2 配置工程
参考各平台文档对工程进行配置，配置完成后才可调用接口使用 GME 服务。

| 平台 | 配置文档 |
|---------|---------|
| Unity | [集成 SDK](https://intl.cloud.tencent.com/document/product/607/10783) |
| Unreal Engine | [集成 SDK](https://intl.cloud.tencent.com/document/product/607/44549) |
| Cocos 2D | [工程配置](https://intl.cloud.tencent.com/document/product/607/15216) |
| Windows | [工程配置](https://intl.cloud.tencent.com/document/product/607/19068) |
| Android | [集成 SDK](https://intl.cloud.tencent.com/document/product/607/40859) |
| iOS | [集成 SDK](https://intl.cloud.tencent.com/document/product/607/15219) |
| Mac | [工程配置](https://intl.cloud.tencent.com/document/product/607/18617) |
| H5 | [工程配置](https://intl.cloud.tencent.com/document/product/607/30261) |

### 7.3 快速接入 SDK
通过快速接入文档，精简接入步骤，快速接入体验功能。快速接入文档中所介绍的功能包括：实时语音、流式语音消息转文本。

| 平台 | 快速接入文档 |
|---------|---------|
| Unity | [Unity SDK 快速接入](https://intl.cloud.tencent.com/document/product/607/44544) |
| Unreal Engine | [Unreal SDK 快速接入](https://intl.cloud.tencent.com/document/product/607/44545) |
| Windows、iOS、Mac、Android | [Native SDK 快速接入](https://intl.cloud.tencent.com/document/product/607/40858) |



### 7.4 基础功能详细接入
根据所使用的平台，[点击](https://www.tencentcloud.com/document/product/607/10780) 查找相应文档进行接入。


### 7.5 接入协助文档
可能会使用到的文档：

| 文档 | 何时使用 |
|---------|---------|
| [音质选择](https://intl.cloud.tencent.com/document/product/607/18522) | 如果对实时语音房间类型选择困难，可以参考这篇文档。 |
| [鉴权密钥](https://intl.cloud.tencent.com/document/product/607/12218) | 希望自己的应用 GME 服务相关的鉴权部署更加安全。 |
| [SDK 版本升级指引](https://intl.cloud.tencent.com/document/product/607/32363) | 从以前的GME版本升级到新的版本，需要查看此文档，了解接口改动。 |
| [错误码](https://intl.cloud.tencent.com/document/product/607/33223) | 接入 SDK 调试的过程中发现接口或者回调返回了错误码，可根据此文档进行解决。 |

## 8. 接入进阶功能


<table>
<thead>
<tr>
<th>如果您想</th>
<th>您可以阅读</th>
</tr>
</thead>
<tbody>
<tr>
<td>在实时语音服务中实现范围语音效果（类似吃鸡游戏全局、小队语音效果）。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/17972" target="_blank">范围语音</a></td>
</tr>
<tr>
<td>根据游戏角色的位置移动，感受到角色的说话声音带有方位的立体声效果，根据距离的远近声音也具有衰减效果，使游戏语音更具沉浸感。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/18218" target="_blank">3D 音效</a></td>
</tr>
<tr>
<td>通过 SDK 接口实现对房间内成员的管理、以及对房间内成员上下麦、禁麦的管理，例如游戏中的队长想要关闭房间内其他玩家的麦克风，或者游戏主播想让听众上麦</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/51115" target="_blank">房间管理功能</a></td>
</tr>
<tr>
<td>利用 GME 在实时语音房间里面播放伴奏，调节伴奏的 EQ，以及播放本地音效。</td>
<td ><a href="https://intl.cloud.tencent.com/document/product/607/31504" target="_blank">实时语音伴奏</a>、<a href="https://intl.cloud.tencent.com/document/product/607/31503" target="_blank">实时语音音效</a>、<a href="https://www.tencentcloud.com/document/product/607/46716" target="_blank">实时语音均衡器</a></td>
</tr>
<tr>
<td>对实时语音进行变声，玩家可将音色调整成“大叔音”、“萝莉音”等形式，增加趣味性</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/44995" target="_blank">语音变声</a></td>
</tr>
<tr>
<td>在实时语音房间中，已经有了小队，又匹配上了其他玩家组了一个匹配队伍，如果想要自己的说话只给小队的人听，又想听到匹配队伍里面路人玩家的声音</td>
<td><a href="https://intl.cloud.tencent.com/document/product/607/39525" target="_blank">音频转发路由</a></td>
</tr>
<tr>
<td>通过语音识别出未成年人语音开黑，解决绕过实名认证和防沉迷系统问题</td>
<td>未成年语音识别</td>
</tr>
<tr>
<td>识别实时语音、音频文件以及语音消息中的涉黄、暴力、谩骂、广告及其它各类敏感或不良信息</td>
<td>实时语音审核、语音消息审核、第三方语音流或音频文件审核</td>
</tr>
<tr>
<td>将玩家的实时语音流转成文本，呈现实时字幕的效果</td>
<td>实时语音转文本</td>
</tr>
</tbody></table>


## 9. 控制台运营指引
有关实时语音、语音消息等服务的用量数据查看，详情可参见 [用量查看](https://intl.cloud.tencent.com/document/product/607/44548)。

## 10. 常见问题
#### 功能相关问题
[使用游戏多媒体引擎实时语音，流量消耗是多少？](https://intl.cloud.tencent.com/document/product/607/39519)
[GME 有哪些功能？](https://intl.cloud.tencent.com/document/product/607/39520)
[GME 的实时语音房间数量和人数有限制吗？](https://intl.cloud.tencent.com/document/product/607/39523)

#### 开发过程中的问题
[GME 可以只使用一个 OpenId 吗？](https://intl.cloud.tencent.com/document/product/607/39521)
[如何使用已下载的 Demo？](https://intl.cloud.tencent.com/document/product/607/39521)
[集成 GME SDK 并导出 Apk 后，启动程序发生黑屏现象，如何解决？](https://intl.cloud.tencent.com/document/product/607/39522)
[在 Xcode 导出可执行文件时，已添加 GMESDK.framework 库，编译时出现编译报错，如何解决？](https://intl.cloud.tencent.com/document/product/607/39522)
[GME SDK 中的 poll 函数应何时开始调用？](https://intl.cloud.tencent.com/document/product/607/30254)



## 11. 出现接入问题

非常抱歉，您接入的过程如果出现了一些问题，可以参考以下思路进行解决：

### 判断问题
首先需要判断问题的类型，根据问题的类型查看相应的文档：[鉴权问题](https://intl.cloud.tencent.com/document/product/607/39824)、[Demo使用问题](https://intl.cloud.tencent.com/document/product/607/39521)、[网络问题](https://intl.cloud.tencent.com/document/product/607/39519) 或者是 [工程导出问题](https://intl.cloud.tencent.com/document/product/607/39522)。

也可以根据使用的服务，判断应该查看的问题文档：

| 使用的服务  | 可以查看的文档 |
|---------|---------|
| 实时语音服务 | [实时语音进房失败问题](https://intl.cloud.tencent.com/document/product/607/39523)、[实时语音无声及音频问题](https://intl.cloud.tencent.com/document/product/607/39524) |
| 语音消息服务 | [语音消息服务问题](https://intl.cloud.tencent.com/document/product/607/39716)|
| 语转文本服务 | [转文本服务问题](https://intl.cloud.tencent.com/document/product/607/39716)|

### 错误码
通过 [错误码](https://intl.cloud.tencent.com/document/product/607/33223) 进行解决，如果出现调用错误，可以查看对应错误码值的原因及解决方案。

举例：在使用 SDK 的过程中，调用 3D 音效相关接口后接口返回 7003 的错误，查看错误码文档可以得知出现此错误码的原因是没有调用 InitSpatializer，可根据此建议排查代码中是否有调用过 InitSpatializer，以及调用的顺序是否正确。

![](https://qcloudimg.tencent-cloud.cn/raw/1394eb8f4947c28728a00c873b3ecb0c.png)

### 寻求帮助
如果通过文档以及错误码无法解决问题，参见 [问题解决指南](https://www.tencentcloud.com/document/product/607/51562) 咨询开发人员。


## 12. 交流与建议
使用腾讯云游戏多媒体引擎产品和服务中有任何问题或建议，您可以通过以下渠道反馈，将有专人跟进解决您的问题：
- 如果发现产品文档的问题，如链接、内容、API 错误等，您可以单击文档页右侧**文档反馈**或选中存在问题的内容进行反馈。
- 如果遇到产品相关问题，您可咨询 [在线客服](https://intl.cloud.tencent.com/contact-sales) 寻求帮助。

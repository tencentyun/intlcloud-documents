
## 功能介绍

安全打击运用自然语言处理技术，针对即时通信 IM 系统中的用户资料、群组资料、单聊文本消息、群聊文本消息，进行网络发文合规判断，自动化、智能化的针对不安全、不适宜的消息内容进行识别。大幅度节省用户的运营成本，为您的产品体验保驾护航。
>!因自定义消息为透传，安全打击功能暂不支持该消息类型进行过滤。

## 安全打击 - 基础版
安全打击 - 基础版为默认开通，仅提供部分涉政类基础词库，不可添加自定义词库，如果您希望使用自定义不雅词功能，您可以在 [即时通信 IM 控制台](https://console.cloud.tencent.com/im)点击【升级】。


## 安全打击 - 高级版
安全打击 - 高级版支持自定义不雅词、不雅词明细查询等功能。

### 开通方式
1. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) ，单击目标应用卡片，在左侧导航栏选择【安全打击】。
2. 单击【升级】即可进入购买页面进行购买。
![](https://main.qcloudimg.com/raw/9bf9e4d9cfd9ed35d8e2a03b9e6585ac.png)
3. 进入购买页后，选择开通安全打击服务，并完成付费，即可开通。
![](https://main.qcloudimg.com/raw/63ece6919e74f17b2056d937dbf7e8ea.png)

### 自定义不雅词
开通__安全打击 - 高级版__之后，控制台内安全打击模块将会开通自定义不雅词功能，选择自定义名单，可进行自定义不雅词的录入。
![](https://main.qcloudimg.com/raw/62554aecad3dd9404d1a6314af633bbe.png)
单击【添加样本】，输入关键词，选择标签，单击【提交】，即可添加自定义不雅词。

>!自定义不雅词一次最多添加50个不雅词，不雅词总计数量不超过3000。单个不雅词不超过10字符。

![](https://main.qcloudimg.com/raw/b7d3bcac627ac3fd877db4ad07f4b6fc.png)
自定义不雅词的标签包括综合、政治、色情、暴恐、谩骂、涉毒、广告。
![](https://main.qcloudimg.com/raw/65c475f9c1652f8fe69fb2f24a684fe2.png)

### 不雅词明细查询
开通__安全打击 - 高级版__之后，单击目标应用卡片，在左侧导航栏选择【安全打击】，单击【明细查询】，可进行不雅词的明细查询。

支持查询任意7日、14日、30日内，任意标签的不雅词的安全打击明细。明细包含打击内容、关键词、审核结果、审核标识和审核时间。
![](https://main.qcloudimg.com/raw/478f6756383e3320f235cc9241373447.png)


## 自定义消息打击
自定义消息安全打击服务需要依靠即时通信 IM 结合第三方安全打击业务。

具体流程为：消息通过 IM SDK 发送至 IM 后台，同时通过第三方消息发送前回调（[单聊](https://intl.cloud.tencent.com/document/product/1047/34364)、[群聊](https://intl.cloud.tencent.com/document/product/1047/34374)），将消息内容抄送至业务后台，业务后台根据第三方安全打击服务要求进行判断，将判断结果告知 IM 后台是否下发。具体方案可参考下图：
![](https://main.qcloudimg.com/raw/34bdd4f7adcb4919c8ef8dc68930ecf2.png)

## 图片、短视频、语音打击
图片、短视频、语音打击安全打击服务需要依靠即时通信 IM 结合第三方安全打击业务。

具体流程为：消息通过 IM SDK 发送至 IM 后台，IM 后台下发消息，同时通过第三方消息发送后回调（[单聊](https://intl.cloud.tencent.com/document/product/1047/34364)、[群聊](https://intl.cloud.tencent.com/document/product/1047/34374)），将消息内容抄送至业务后台，业务后台根据第三方安全打击服务要求进行判断，将判断结果告知 IM 后台是否撤回 [单聊消息](https://intl.cloud.tencent.com/document/product/1047/35015)、[群聊消息](https://intl.cloud.tencent.com/document/product/1047/34965)。具体方案可参考下图：
![](https://main.qcloudimg.com/raw/f934c972855307282bba88f77ddbaf47.png)

## 简介

目前，厂商会逐步对 App 开发者的通知消息根据分类进行限额限频，以此保证终端用户不被过度骚扰，不同的消息分类主要通过渠道 ID（ChannelID）进行区分。移动推送综合各厂商的分类能力，支持将消息分为两类：

- 普通消息（默认）：适用于推送全员公告、运营活动、热点新闻等，多为用户普适性的内容。
- 通知消息/个人私信：适用于推送聊天消息、个人订单变化、交易提醒等与私人通知相关的内容，通知消息的推送数量不受限制。

消息分类支持在调用推送 API 时指定。
魅族暂不支持消息分类，且不限额。

#### 使用步骤

1. 若需要使用厂商通知消息，按以下说明申请或创建通知消息的 Channel ID：
	- [OPPO 申请指南](#oppozhinan)
	- [小米申请指南](#xiaomizhinan)
	- [vivo 申请指南](#vivozhinan)
	- [华为使用指南](#huaweizhinan)
	- [荣耀使用指南](#rongyaozhinan)
>?从 Android 8.0（API 级别 26）开始，弹出通知栏通知必须先为应用创建通知渠道，并为要弹出的通知分配渠道，否则通知将不会显示。通过将通知分配给特定的通知渠道，则该通知将以该通知渠道已被开启的行为功能展示在通知栏中。用户可以为应用的每个通知渠道进行个性化控制，而非直接管理应用的所有通知，例如控制每个渠道的开闭、视觉和听觉选项等。
>一个应用可以有多个通知渠道，建议设置不超过7个通知渠道。应用的每个通知渠道按照通知渠道id（channel_id）区分，通知渠道以通知渠道名称（channel_name）定义的文本展示在应用的通知设置中。
>通知渠道一旦创建，设备用户拥有完全控制权，开发者便无法更改通知行为。对同一个通知渠道id（channel_id）进行重复创建的代码调用，仅不同的通知渠道名称（channel_name）和渠道描述参数会生效，其他的视觉、听觉、重要性等选项无法改变。
>

2. 若需要使用厂商做渠道分类管理，自定义 Channel ID，从而做到根据 App 自身的业务消息类别进行消息分类，可根据不同厂商对应进行配置：
<table>
<thead>
<tr>
<th>推送通道</th>
<th>配置说明</th>
</tr>
</thead>
<tbody><tr>
<td>移动推送自建通道</td>
<td><ul><li>App 端，调用 Android SDK 创建 Channel ID 接口创建 Channel ID。</li><li>调用移动推送 <a href="https://intl.cloud.tencent.com/document/product/1024/33764">服务端 API</a> 时，指定对应的 Channel ID（不限额度）。</li></ul></td>
</tr>
<tr>
<td>华为</td>
<td><ul><li>在华为管理台 <a href = "https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-classification-0000001149358835#section1653845862216">申请自分类权益</a>，自分类权益生效后，应用的推送消息将根据hw_category字段进行归类。。</li><li>调用移动推送 <a href = "https://intl.cloud.tencent.com/document/product/1024/33764">服务端 API</a> 时，指定 hw_category 参数。</li><li>华为的 ChannelID 作为自定义的渠道策略展示消息提醒方式，不作消息分类。</li></ul></td>
</tr>
<tr>
<td>小米</td>
<td><ul><li> 在小米开放平台管理台上创建 Channel ID 或通过小米服务端 API 创建。</li><li>调用移动推送 <a href="https://intl.cloud.tencent.com/document/product/1024/33764">服务端 API</a> 时，指定对应的 Channel ID。 </li></td>
</tr>
<tr>
<td>OPPO</td>
<td><ul><li>App 端，调用 Android SDK 创建 Channel ID。</li><li>在 OPPO 管理台登记该 Channel ID，保持一致性.</li><li>调用移动推送 <a href="https://intl.cloud.tencent.com/document/product/1024/33764">服务端 API</a> 时，指定对应的 Channel ID。</li></ul></td>
</tr>
<tr>
<td>魅族</td>
<td>无 Channel 相关说明。</td>
</tr>
<tr>
<td>vivo</td>
<td><ul><li>支持配置使用 vivo 系统消息/运营消息，不支持自定义通知渠道 Channel 。</li><li>调用移动推送 <a href="https://intl.cloud.tencent.com/document/product/1024/33764">服务端 API</a> 时，指定vivo_ch_id参数传值”</li></ul></td>
</tr>
<tr>
<td>荣耀</td>
<td><ul><li>支持配置使用 荣耀 服务通讯/资讯营销消息，不支持自定义通知渠道 Channel 。</li><li>调用移动推送 <a href="https://intl.cloud.tencent.com/document/product/1024/33764">服务端 API</a> 时，指定hw_importance参数传值”</li></ul></td>
</tr>
</tbody></table>
3. 若既不需要使用厂商通知消息，也不需要自定义 Channel ID，则无需做任何处理，移动推送会为 App 的所有消息指定一个默认的 Channel ID，消息归到默认类别中。

## OPPO 通知渠道申请指南[](id:oppozhinan)

### OPPO 通知渠道介绍

OPush 平台上默认的是公信通道，目前在原有基础上新增“私信”通道，对单个用户推送个性化信息时，不再受推送数量限制。以下是“公信”和“私信”的对比：
<table>
<thead>
<tr>
<th colspan = "2">类型</th>
<th>公信</th>
<th>私信</th>
</tr>
</thead>
<tbody><tr>
<td colspan = "2">推送内容</td>
<td>热点新闻、新品推广、平台公告、社区话题、有奖活动等，多用户普适性的内容。</td>
<td>个人订单变化、快递通知、订阅内容更新、评论互动、会员积分变动等，与单个用户信息强相关的内容。</td>
</tr>
<tr>
<td rowspan = "2">单用户推送限制（条/日）</td>
<td>新闻类（三级分类为新闻类）</td>
<td>5条</td>
<td>不限量。</td>
</tr>
<tr>
<td>其他应用类型</td>
<td>2条</td>
<td>不限量。</td>
</tr>
<tr>
<td colspan = "2">推送数量限制</td>
<td>所有公信类通道共享推送次数，当日达到次数限制后，所有公信类通道将不能再推送消息，目前单日推送数量为：累计注册用户数 * 2 。</td>
<td>不限量。</td>
</tr>
<tr>
<td colspan = "2">配置方式</td>
<td>默认。</td>
<td>需要在 OPPO PUSH 运营平台上登记该通道，并将通道对应属性设置为“私信” 。</td>
</tr>
</tbody></table>

>! OPPO 官方提醒：切记！一定不要利用私信通道用于普适性消息推送（如热点新闻、新品推广等），后台会实时监控，如违反运营规则，OPush 有权关闭您的私信通道权限。由此产生的后果，如调用接口异常，或使用私信通道发送的消息没到达用户等，由业务方自行承担。
>

### OPPO 私信通道申请
[](id:localtion)

1. 进入 [OPPO 开放平台](https://push.oppo.com)，在**应用配置**>**新建通道**中新建通道，通道 ID 与通道名称必填且需要与应用客户端保持一致，其他选项可不填。
>! 通道 ID 一旦确定下来不能随意变更或删除。
>
![](https://main.qcloudimg.com/raw/20c0242e7558cdfac1bd6d6a79f0a219.png)
2. 目前 OPPO 私信通道需要邮件申请后才能生效，请按照以下要求发送邮件给 OPush 平台，详情请参见 [OPPO PUSH 通道升级公测邀请](https://open.oppomobile.com/new/developmentDoc/info?id=11227)。


### OPPO 私信通道使用

1. 客户端创建通知渠道，请选择以下任意一种方式创建：
	1. 使用 Android API 创建通知渠道，详见 Android 官方文档 [创建和管理通知渠道](https://developer.android.google.cn/training/notify-user/channels)。
	2. 使用移动推送SDK（1.1.5.4及以上的版本）创建通知渠道，详见文档 [创建通知渠道](https://intl.cloud.tencent.com/document/product/1024/30715)。
2. Rest API 推送。
在 Rest API 请求参数 Android 结构体中设置 `oppo_ch_id` 参数，可实现根据通知渠道下发，具体参见 [PushAPI 参数说明](https://intl.cloud.tencent.com/document/product/1024/33764)。
>! 目前 OPPO 私信通道通知只能通过 Rest API 进行下发，控制台暂不支持。
>
推送示例如下：
<dx-codeblock>
:::  json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a1c2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
    "title": "测试标题",
    "content": "测试内容",
    "android": {
        "oppo_ch_id": "私信通道id"}
  }
}
:::
</dx-codeblock>

## 小米通知渠道申请指南[](id:xiaomizhinan)

### 小米通知渠道介绍 	

小米推送（Mipush）的通知渠道分为“私信消息”和“公信消息”两类，不同类别对应不同的权限，详情请参见 [小米推送消息分类新规](https://dev.mi.com/distribute/doc/details?pId=1655)。

- 公信消息适用于推送热点新闻、新品推广、平台公告、社区话题、有奖活动等，多为用户普适性的内容。
- 私信消息适用于推送聊天消息、个人订单变化、快递通知、交易提醒、IOT 系统通知等与私人通知相关的内容，通知消息的推送数量不受限制。
小米推送对推送消息数量、推送速率 QPS 进行了统一管理，详情请参见 [小米推送消息限制说明](https://dev.mi.com/distribute/doc/details?pId=1656#_2)。

公信消息与私信消息限制说明：

<table>
<thead>
<tr>
<th>消息类型</th>
<th>消息内容</th>
<th>用户接收数量限制</th>
<th>申请方式</th>
</tr>
</thead>
<tbody><tr>
<td>默认</td>
<td>可按照小米的 <a href="https://dev.mi.com/distribute/doc/details?pId=1655#_3">公信场景说明</a></td>
<td>单个应用单个设备单日一条</td>
<td>无需申请</td>
</tr>
<tr>
<td>公信消息</td>
<td>热点新闻、新品推广、平台公告、社区话题、有奖活动等，多用户普适性的内容。</td>
<td>单个应用单个设备单日5-8条。</td>
<td rowspan="2">需在小米推送平台申请，详情请参见 <a href="https://dev.mi.com/distribute/doc/details?pId=1655#_4">channel 申请及接入方式</a>。</td>
</tr>
<tr>
<td>私信消息</td>
<td>聊天消息、个人订单变化、快递通知、交易提醒、IoT系统通知等与私人通知相关的内容。</td>
<td>不限量</td>
</tr>
</tbody></table>

### 小米额外提升推送量级申请

目前小米通知消息需要开发者登录小米推送运营平台，在**应用管理**>**通知类别**菜单页面进行申请操作，详情请参见 [小米推送通知消息](https://dev.mi.com/console/doc/detail?pId=2086#_0_1)。

>!为了规范使用小米推送，请准守小米的 [推送营运规则](https://dev.mi.com/distribute/doc/details?pId=1657)。
>

### 小米通知消息使用

目前小米通知消息只能通过 Rest API 进行下发，控制台暂不支持。
在 Rest API 请求参数 `Android` 结构体中设置 `xm_ch_id ` 参数，可实现小米通知渠道下发，详情请参见 [PushAPI](https://intl.cloud.tencent.com/document/product/1024/33764) 参数说明。
推送示例如下：

```json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
     "title": "小米通知消息",
     "content": "测试内容",
     "android": {
        "xm_ch_id": "小米通知消息的channel_id"
     }
	   }
}
```

<span id="vivozhinan"> </span>
## vivo 系统消息申请指南

### vivo 消息分类介绍

vivo 消息分类功能将推送消息类型分为运营消息和系统消息。
为提升用户消息通知体验，营造良好推送生态，vivo 推送服务于2023年4月3日起，针对不同应用类别的消息进行统一管理，详情请参见 vivo 的 [推送消息限制说明](https://dev.vivo.com.cn/documentCenter/doc/695)。

<table>
<thead>
<tr>
<th colspan = "2">消息分类</th>
<th>应用类别</th>
<th>推送数量限制</th>
<th>用户接收数量限制</th>
</tr>
</thead>
<tbody><tr>
<td colspan = "2">系统消息</td>
<td>/</td>
<td>3倍通知开启有效用户数
（可邮件申请消息不限量权限）</td>
<td>无限制</td>
</tr>
<tr>
<td  colspan = "2" rowspan = "2">运营消息</td>
<td>新闻类
（具备《互联网新闻信息服务许可证》）</td>
<td>3倍通知开启有效用户数</td>
<td>5条</td>
</tr>
<tr>
<td>其他类</td>
<td>2倍通知开启有效用户数</td>
<td>2条</td>	
</tr>
</tbody></table>

推送数量超过当日限制时，返回错误码10070或10073，10070：运营消息发送量总量超出限制；10073：系统消息发送量总量超出限制。

> ?
>1. 2020年6月1日前，无论是否接入消息分类，频控规则不变，均按每个应用单用户“公共类消息（全推，群推，标签推）”每天接收上限为5条，不限制单推条数。2020年6月1日起，频控规则变更为按每个应用单用户“运营消息”接收条数上限5条进行频控，若出现用户体验类投诉，将会根据实际情况调整条数。
>2. Funtouch OS_10及以上版本没有消息盒子，应用不存活时窄条展示，具体样式以实际为准。
>3. 系统消息量级和运营消息量级均会随着 SDK 订阅数变化而自动变化，如特殊情况需额外提升系统消息量级，申请方法详见下方 **[vivo 系统消息申请](#vivo_system)**。
>4. 若某 vivo 用户当前接收运营消息超过5条，则当天触发限额后的运营消息均会通过移动推送自建通道下发，不再通过 vivo 通道下发。
>5. 若您已向 vivo 申请提升运营消息限额，请联系我们进行后台配置，否则限额变更无法生效。
>

[](id:vivo_system)
### vivo 系统消息申请

系统消息量默认是3倍的 SDK 订阅数，当系统消息不够时，可以邮件按实际需求 [申请系统消息](https://dev.vivo.com.cn/documentCenter/doc/359) 量级，按照下面的邮件模板填写信息后发送至邮箱：push@vivo.com。
```plaintext
主题：xxx应用申请增加im消息/系统消息发送量级
正文：……
应用名称：……
包名：……
应用简介：……
IM消息/系统消息需求量级（万）：……
具体推送场景说明：例如，用户个人聊天、商家聊天
```

### vivo 系统消息使用

目前 vivo 通知消息只能通过 Rest API 进行下发，控制台暂不支持。
在 Rest API 请求参数 `Android` 结构体中设置 `vivo_ch_id ` 参数为"1"，可实现 vivo 系统消息下发，详情请参见 [PushAPI](https://intl.cloud.tencent.com/document/product/1024/33764) 参数说明。
>?
>- vivo 推送平台将按消息分类标准，对系统消息进行每日巡检，巡查开发者以系统消息渠道发送运营消息的情况，并按违规程度及频次进行相应处罚，最高将关闭消息推送功能。
>- 请开发者参见 [消息分类功能](https://dev.vivo.com.cn/documentCenter/doc/359) 文档，严格按照平台消息分类运营。具体处罚规则：消息分类功能说明>五.运营监管及处罚>3.处罚标准。

推送示例如下：

```json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
     "title": "vivo系统通知",
     "content": "测试内容",
     "android": {
        "vivo_ch_id": "1"
     }
   }
}
```

<span id="huaweizhinan"> </span>

## 华为消息分类使用指南

### 华为消息分类介绍

华为推送从 EMUI 10.0版本开始将通知消息智能分成两个级别：「服务与通讯」和「资讯营销」。EMUI 10.0之前的版本没有对通知消息进行分类，只有一个级别，消息全部通过“默认通知”渠道展示，等价于 EMUI 10.0的服务与通讯。资讯营销类消息的每日推送数量自2023年01月05日起根据应用类型对推送数量进行上限管理，服务与通讯类消息每日推送数量不受限。
华为回执 256 表示当日的发送量超出资讯营销类消息的限制，请您调整发送策略，各消息类型详情请参见华为的 [推送数量关系细则](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-restriction-description-0000001361648361?ha_source=hms5)。如图所示：
![](https://qcloudimg.tencent-cloud.cn/raw/8b5ded2fd11711c69227432e9eb0c571.png)

不同消息级别呈现样式对比：

| 消息级别 | 在通知中心的显示 | 在状态栏上显示 | 锁屏通知 | 响铃 | 振动 |
| -------- | ---------------- | -------------- | -------- | ---- | ---- |
| 服务与通讯     | 正常显示         | 支持           | 支持     | 支持 | 支持 |
| 资讯营销     | 正常显示         | 否             | 否       | 否   | 否   |

若您希望服务与通讯类消息也按照静默的方式发送，可以添加hw_importance字段且传值为“1”，详情请参见 [PushAPI](https://intl.cloud.tencent.com/document/product/1024/33764) 参数说明。

分类规则：

- 消息智能分类
智能分类算法将根据您发送的内容等多个维度因素，自动将您的消息按照分类标准进行归类。
- 消息自分类
2021年7月1日起，华为推送服务开始接收开发者自分类权益的申请。申请成功后，允许开发者根据华为推送分类规范，自行对消息进行分类。

### 自分类消息权益申请
华为通知消息自分类权限需要申请后才能生效，详情请参见 [消息分类方式](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/message-classification-0000001149358835#section1653845862216)。

>!
> - 若应用没有自分类权益，则应用的推送消息将通过智能分类进行自动归类。
> - 若应用有自分类权益，将信任开发者提供的分类信息，消息不经过智能分类。
> 

### 自分类消息使用

自分类消息仅支持 API 进行下发，控制台暂不支持，在您自分类消息申请后，可通过以下方式使用：

在 Rest API 请求参数 `Android` 结构体中设置 `hw_category ` 参数，可实现华为自分类消息下发，详情请参见 [PushAPI](https://intl.cloud.tencent.com/document/product/1024/33764) 参数说明。

推送示例如下：

```json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
        "title": "帐号下线：",
        "content": "您的帐号出现异地登录，已经下线。",
        "android": {
            "hw_category":"VOIP"
        }
    }
}
```

### 华为通知渠道创建

华为推送支持应用自定义通知渠道，客户端创建通知渠道，请选择以下任意一种方式创建：

1. 使用 Android API 创建通知渠道，详情请参见 Android 官方文档 [创建和管理通知渠道](https://developer.android.google.cn/training/notify-user/channels)。
2. 使用移动推送SDK（1.1.5.4及以上的版本）创建通知渠道，详情请参见文档 [创建通知渠道](https://intl.cloud.tencent.com/document/product/1024/30715)。

### 华为通知渠道使用

目前自定义渠道只能通过 Rest API 进行下发，控制台暂不支持，在您创建完成通知渠道后，可通过以下方式使用：

在 Rest API 请求参数 `Android` 结构体中设置 `hw_ch_id ` 参数，可实现华为通知渠道下发，详情请参见 [PushAPI](https://intl.cloud.tencent.com/document/product/1024/33764) 参数说明。

>! 
> - 如果您的应用在华为推送控制台申请开通华为推送服务时，选择的数据处理位置为中国区，自定义渠道功能将不再适用于您的应用。您的推送消息将按照智能分类系统或消息自分类权益确认的消息级别，归类为服务与通讯类或资讯营销类消息。详见 [自定义通知渠道](https://developer.huawei.com/consumer/cn/doc/development/HMSCore-Guides/android-custom-chan-0000001050040122)。
> - 自定义渠道功能需要您的应用具有消息自分类权益，请参见上文进行申请。
>

推送示例如下：

```json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
        "title": "华为通知消息",
        "content": "测试内容",
        "android": {
            "hw_ch_id": "华为通知消息的channel_id"
        }
    }
}
```

[](id:rongyaozhinan)
## 荣耀消息分类使用指南

### 荣耀消息分类介绍

荣耀推送服务将根据应用类型、消息内容和消息发送场景，将推送消息分成服务通讯和资讯营销两大类别，资讯营销类消息的每日推送数量根据应用类型对推送数量进行上限管理，服务与通讯类消息每日推送数量不受限，详细说明请参见 [荣耀推送数量管理细则](https://developer.hihonor.com/cn/kitdoc?category=%E5%9F%BA%E7%A1%80%E6%9C%8D%E5%8A%A1&kitId=11002&navigation=guides&docId=notification-push-standards.md&token=)。
根据消息分类，对不同类别消息的默认展示方式、消息样式进行差异化管理，具体如下：

| 消息级别 | 通知栏下拉的显示 | 图标显示 | 锁屏通知 | 响铃 | 振动 |
| -------- | ---------------- | -------------- | -------- | ---- | ---- |
| 服务与通讯     | 正常显示         | 支持           | 支持     | 支持 | 支持 |
| 资讯营销     | 正常显示         | 否             | 否       | 否   | 否   |

- importance 字段值为“1”时：表示消息为资讯营销类，默认展示方式为静默通知，仅在下拉通知栏展示。
- importance 字段值为“2”时：表示消息为服务通讯类，默认展示方式为锁屏展示+下拉通知栏展示。

分类规则：

- 消息智能分类
智能算法将根据APP类型和消息内容等维度，自动将您的消息按照分类标准进行归类。
- 消息自分类
允许开发者根据消息分类规范，自行对消息进行分类。
目前，所有消息默认通过消息自分类方式进行分类处理，荣耀推送服务将充分信任开发者提供的分类结果，并展示对应信息。随着荣耀推送服务能力的不断补充和演进，分类方式也会逐渐更新与升级，请参见 [荣耀最新分类说明](https://developer.hihonor.com/cn/kitdoc?category=%E5%9F%BA%E7%A1%80%E6%9C%8D%E5%8A%A1&kitId=11002&navigation=guides&docId=notification-class.md&token=)。

>!请遵守荣耀的推送分类规则，违规者将受到荣耀对应的处罚，违规行为及相应的处罚措施请参见 [消息违规处罚标准](https://developer.hihonor.com/cn/kitdoc?category=%E5%9F%BA%E7%A1%80%E6%9C%8D%E5%8A%A1&kitId=11002&navigation=guides&docId=notification-penalty-standards.md&token=)。
> 

### 自分类消息使用

自分类消息仅支持 API 进行下发，控制台暂不支持，可通过以下方式使用：

在 Rest API 请求参数 `Android` 结构体中设置 `hw_importance ` 参数，可实现荣耀自分类消息下发，详情请参见 [PushAPI](https://intl.cloud.tencent.com/document/product/1024/33764) 参数说明。

推送示例如下：

```json
{
    "audience_type": "token",
    "token_list": ["005c28bf60e29f9a***2052ce96f43019a0b7"],
    "message_type": "notify",
    "message": {
        "title": "荣耀：",
        "content": "自分类推送。",
        "android": {
            "hw_importance":2
        }
    }
}
```





## TUIKit 介绍
TUIKit 是基于腾讯云 IM SDK 的一款 UI 组件库，它提供了一些通用的 UI 组件，包含会话、聊天、搜索、关系链、群组、音视频通话等功能。
基于 UI 组件您可以像搭积木一样快速搭建起自己的业务逻辑。
TUIKit 中的组件在实现 UI 功能的同时，会调用 IM SDK 相应的接口实现 IM 相关逻辑和数据的处理，因而开发者在使用 TUIKit 时只需关注自身业务或个性化扩展即可。


## TUIKit 主要功能介绍
TUIKit 按照功能主要分为**聊天**、**关系链**、**用户或群组资料**、**搜索**、**语音**几个类型的 UI 组件，每个类型的 UI 组件负责展示不同的内容。具体的 UI 组件描述如下表所示：

| 组件名               | 组件功能           |
| -------------------- | ------------------ |
| TIMUIKitConversation | 会话列表组件       |
| TIMUIKitChat         | 聊天组件           |
| TIMUIKitAddFriend    | 添加好友组件       |
| TIMUIKitAddGroup     | 添加群组组件       |
| TIMUIKitBlackList    | 黑名单列表组件     |
| TIMUIKitContact      | 好友列表组件       |
| TIMUIKitGroup        | 群组列表组件       |
| TIMUIKitGroupProfile | 群组信息组件       |
| TIMUIKitNewContact   | 新的联系人列表组件 |
| TIMUIKitProfile      | 用户信息组件       |
| TIMUIKitSearch / TIMUIKitSearchMsgDetail      | 全局搜索/会话内搜索组件           |


界面效果如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/b3d5bba6d133d3a0f3a4fa7534037f01.png" style="zoom:50%;"/>

<img src="https://qcloudimg.tencent-cloud.cn/raw/33d706da1fd69cbe92c7dd95357f9486.png" style="zoom:50%;"/>

### TIMUIKitChat 重点功能介绍
TIMUIKitChat 主要负责消息界面的展示。您可以利用它直接发送不同类型的消息，进行消息表情回应/回复/引用、查询消息已读回执详情等。
界面效果如下图所示：
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">消息界面</th>
    <th style="text-align:center;" width="500px">发送多种类型消息</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/9efa78f5687481ab901863dfaeb144d4.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/bc1c20996f6618ee8fee3c55fe78535f.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">表情回应/回复/引用</th>
    <th style="text-align:center;" width="300px">文件自动匹配icon</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/04c0e4192ca8d62bc6bc1e34b93813b7.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/c5ba69d29764269cab6262a0982bad97.png" /></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">消息已读回执</th>
    <th style="text-align:center;" width="300px">已读回执详情</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/e15f2913e6f04a9ff914bcf1a6fc6952.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/44277387d4df1861e11cc41654f5cf24.png" /></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">群tips消息</th>
    <th style="text-align:center;" width="300px">入群申请审批</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/d9895126af46a910586c600aadc475b6.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/42ba9e61d3cfc5795b17cc89e6b8c248.png" /></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">链接解析</th>
    <th style="text-align:center;" width="300px">地理位置消息</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/87a331a8f56326b53eebda543bc89250.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/d85fb829caf15ca55c63958e1dcb1247.png" /></td>
	 </tr>
</table>

### 关系链 重点功能介绍
关系链主要负责当前用户的联系人、群聊、黑名单的信息展示。
界面效果如下图所示：
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">联系人列表(TIMUIKitContact)</th>
    <th style="text-align:center;" width="500px">新的联系人列表(TIMUIKitNewContact)</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/a5b16c58dc6f07245d9c812ed73f0c06.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/cc507ea91ac78c57d7fedf34f804857a.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">参与的群聊列表(TIMUIKitGroup)</th>
    <th style="text-align:center;" width="300px">黑名单列表(TIMUIKitBlackList)</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/331cc34016bc624819fd249577793e74.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/cc619a08dfe4da2307b8cb3086731e9c.png" /></td>
	 </tr>
</table>

### TIMUIKitConversation 重点功能介绍
TIMUIKitConversation 主要负责会话列表的展示和编辑。
界面效果如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/53880bb394b8b665fec6724f16d286ee.png" style="zoom:40%;"/>

### TIMUIKitProfile 重点功能介绍
TIMUIKitProfile 主要负责联系人的资料展示与管理。
界面效果如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/338aa97bdc58f79fd49e5cfc1ed1c93c.png" style="zoom:40%;"/>


### 添加用户与群组 功能介绍
TIMUIKitAddFriend为添加好友页面。
TIMUIKitAddGroup为添加群组页面。
界面效果如下图所示：
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">添加好友页面(TIMUIKitAddFriend)</th>
    <th style="text-align:center;" width="500px">添加群组页面(TIMUIKitAddGroup)</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/bb42196224b3bc2ec5fe69654622da34.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/5d3f91b40ee4226637f41215e6b625f1.png"/></td>
	 </tr>
</table>

### TIMUIKitGroupProfile 重点功能介绍
TIMUIKitGroupProfile 主要负责群资料、群成员、群组权限的展示与管理。
界面效果如下图所示：
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="500px">群资料及管理</th>
    <th style="text-align:center;" width="500px">群成员管理</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/ae5e50eb857308403d802fed9cbffb83.png"/></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/a25514e0bab675b5f5e356604310bcb5.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">加群方式管理</th>
    <th style="text-align:center;" width="300px">群操作</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/78d9a2eae2b8f95226075b1f676f9984.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/197466803785eeb07297d68a68e2872a.png" /></td>
	 </tr>
</table>


### 本地搜索 重点功能介绍
TIMUIKitSearch 为本地全局搜索，支持搜索联系人、群聊、聊天记录。
TIMUIKitSearchMsgDetail 为会话内聊天历史记录搜索。
详情[可查看此文档](https://intl.cloud.tencent.com/document/product/1047/50036)，界面效果如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/35a45f8176005b46e67020e5d9656d0a.png" style="zoom:40%;"/>

### 音视频通话 重点功能介绍
[音视频通话插件插件](https://pub.dev/packages/tim_ui_kit_calling_plugin) 主要负责语音、视频通话。
单聊语音通话示意图：
<img src="https://qcloudimg.tencent-cloud.cn/raw/78c9aa0717517f9e2c245dba1267771e.png" style="zoom:40%;"/>
单聊视频通话示意图：
<img src="https://qcloudimg.tencent-cloud.cn/raw/7ad0a4b83db9c29053207af0f9af3834.png" style="zoom:45%;"/>
群聊语音与视频通话示意图：
<img src="https://qcloudimg.tencent-cloud.cn/raw/5337679a405abee981d094cd33795a7e.png" style="zoom:42%;"/>

您可以在 TIMUIKitChat 消息页、TIMUIKitProfile 个人资料页等页面启动语音、视频通话。
界面效果如下图所示：
<table style="text-align:center; vertical-align:middle; width:1000px">
  <tr>
    <th style="text-align:center;" width="300px">消息页启动</th>
    <th style="text-align:center;" width="300px">资料页启动</th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/fab20b828cf3cb8417d169e890b1b0c6.png" /></td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/b1ba063e4ee5bee45c168c799c800a7b.png" /></td>
	 </tr>
</table>


### 消息推送重点功能介绍
你可通过我们的[Flutter 推送插件](https://intl.cloud.tencent.com/document/product/1047/50032)集成消息推送能力，涵盖离线推送与在线推送。
消息推送效果如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/9634f4ffa77a91c8c95c73091abb38ae.png" style="zoom:40%;"/>

[](id:feedback)

## 联系我们

如果您有任何进一步的问题或想要了解更多有关用例的信息，请不要犹豫，在以下位置与我们联系。

[Telegram Group](https://t.me/+1doS9AUBmndhNGNl)
[WhatsApp Group](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)

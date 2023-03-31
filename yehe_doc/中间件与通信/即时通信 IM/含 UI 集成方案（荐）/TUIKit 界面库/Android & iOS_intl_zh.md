## TUIKit 介绍
TUIKit 是基于腾讯云 IM SDK 的一款 UI 组件库，它提供了一些通用的 UI 组件，包含会话、聊天、搜索、关系链、群组、音视频通话等功能。
基于 UI 组件您可以像搭积木一样快速搭建起自己的业务逻辑。
TUIKit 中的组件在实现 UI 功能的同时，会调用 IM SDK 相应的接口实现 IM 相关逻辑和数据的处理，因而开发者在使用 TUIKit 时只需关注自身业务或个性化扩展即可。
TUIKit 从 6.9.3557 版本开始新增了全新的简约版 UI 组件，之前版本 UI 组件依旧保留，我们称之为经典版 UI 组件，您可以根据需求自由选择经典版或简约版 UI 组件。

## TUIKit 主要功能介绍
TUIKit 主要分为 TUISearch、TUIConversation、TUIChat、TUICallKit、TUIContact、TUIGroup 和 TUIOfflinePush 几个 UI 子组件，每个 UI 组件负责展示不同的内容。
界面效果如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/9c893f1a9c6368c82d44586907d5293d.png" style="zoom:50%;"/>

### TUIChat 重点功能介绍
TUIChat 主要负责消息界面的展示。您还可以利用它直接发送不同类型的消息、对消息长按点赞/回复/引用、查询消息已读回执详情等。
界面效果如下图所示：

<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">消息界面 | 发送多种类型消息</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/5684d3acaf42b95cc942dad24980e129.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">消息点赞 | 回复  </th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/f457d0855163c13c1e12a06b13e54e3e.png" /></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">消息已读回执 | 已读回执详情</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/00e2ed68b44bd9406732674eeb3164f9.png" /></td>
	 </tr>
</table>


### TUIContact 重点功能介绍
TUIContact 主要负责联系人的展示、权限设置等。
界面效果如下图所示：

<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">关系链列表 | 联系人资料及管理</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/fde8afab364cef589ffe9f059aede058.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">参与的群聊列表 | 黑名单列表</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/140f2dd618e8eb26a434277cbdac7fe3.png" /></td>
	 </tr>
</table>

### TUIConversation 重点功能介绍
TUIConversation 主要负责会话列表的展示和编辑。
界面效果如下图所示：
<img src="https://qcloudimg.tencent-cloud.cn/raw/f421db60d6a85bb948217ffdfc7836a9.png" style="zoom:40%;"/>


### TUIGroup 重点功能介绍
TUIGroup 主要负责群资料、群成员、群组权限的管理。
界面效果如下图所示：


<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">群资料及管理 | 群成员管理</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/88b77b431ac007a0c9a5f913c0e73a0c.png"/></td>
	 </tr>
</table>
<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">加群方式管理 | 权限管理</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/24afe0858bfda4fca3e11626341a1954.png" /></td>
	 </tr>
</table>




### TUISearch 重点功能介绍
TUISearch 主要负责本地搜索，支持搜索联系人、群聊、聊天记录。
界面效果如下图所示：


<img src="https://qcloudimg.tencent-cloud.cn/raw/0c70b9d8abbb494a51d152438e195fbf.png" style="zoom:40%;"/>

### TUICallKit 重点功能介绍
TUICallKit 主要负责语音、视频通话。
单聊通话示意图：

<table style="text-align:center;vertical-align:middle;width:600px">
  <tr>
    <th style="text-align:center;" width="600px">视频通话<br></th>
    <th style="text-align:center;" width="600px">语音通话<br></th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/44d4c8a412752abda898341665a90016.png"  />    </td>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/5eb84936666da81b0331a28c3c779b77.png" />     </td>
	 </tr>
</table>



群聊通话示意图：
<table style="text-align:center;vertical-align:middle;width:600px">
  <tr>
    <th style="text-align:center;" width="600px">视频通话<br></th>
    <th style="text-align:center;" width="600px">语音通话<br></th>
  </tr>
  <tr>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/83d6cd991cd0e9251caafebe75e46f12.png"  />    </td>
    <td><img style="width:500px" src="https://qcloudimg.tencent-cloud.cn/raw/842c563a9dd99da4950402e7a61836dd.png" />     </td>
	 </tr>
</table>

如果您集成了 TUIChat、TUIContact 及 TUICalllKit，您可以在 TUIChat 消息页、TUIContact 个人资料页启动语音、视频通话。
界面效果如下图所示：

<table style="text-align:center; vertical-align:middle; width:600px">
  <tr>
    <th style="text-align:center;" width="600px">消息页启动 | 资料页启动</th>
  </tr>
  <tr>
    <td><img style="width:600px" src="https://qcloudimg.tencent-cloud.cn/raw/0302a0a9eed1c58ef14f05d3f17d96c4.png" /></td>
	 </tr>
</table>


### TUIOfflinePush 重点功能介绍
TUIOfflinePush 主要负责离线推送消息展示。
离线推送效果如下图所示：
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/CFL3713_TUIofflinepush.png" style="zoom:90%;"/>

[](id:feedback)

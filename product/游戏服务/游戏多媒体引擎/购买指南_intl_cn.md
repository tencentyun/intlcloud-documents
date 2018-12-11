目前游戏多媒体引擎 GME 提供实时语音、语音消息及转文本服务，各项服务的价格信息如下。


## 实时语音服务
普通音质按语音 DAU 计费，高清音质按语音时长计费。

- 对战、休闲类游戏场景推荐选择普通音质。
- 语音直播、K 歌场景推荐选择高清音质。

### 免费体验须知
实时语音服务的两种计费模式，免费体验的范围如下：
- 按语音 DAU 计费，单日语音 DAU 不超过100人则免费。
- 按语音时长计费，单日语音时长不超过300分钟则免费。

若超过上述限制，则需按用量付费。

>?若某应用单日实时语音时长为150分钟则免费。若单日实时语音时长为1000分钟，则计费时长为1000分钟。费用 = 1000分钟 \* 0.0059/分钟 = 5.9元（按语音时长计费单价为0.0059元/分）。


### 价格表
<table>
   <tr>
      <td rowspan="8">按语音 DAU 计费</td>
      <td  rowspan="4">付费区间</td>
      <td rowspan="2">语音 DAU</td>
      <td>In Mainland China (USD/DAU/day)</td>
      <td>Outside Mainland China (USD/DAU/day)</td>
   </tr>
   <tr>
      <td>0.0015</td>
      <td>0.0072</td>
   </tr>
   <tr>
      <td >免费区间</td>
      <td   colspan="4">DAU≤100</td>
   </tr>
</table>



<table>
   <tr>
      <td rowspan="3">按语音时长计费</td>
      <td rowspan="2">付费区间</td>
      <td colspan="4">Unit Price (USD/1,000 minutes)</td>
   </tr>
   <td colspan="2">0.94</td>
   <tr>
      <td>免费区间</td>
      <td >时长≤300分钟</td>
   </tr>
</table>



>!
- 应用内用户进入房间即算作语音 DAU，语音 DAU 按照 openID 去重计算（openID 是应用内用户的唯一标识符，一个用户对应一个 openID）。
- 应用内用户进入房间即算语音时长。若 A 用户在 12:00 时进入语音房间，B 用户在 12:30 时进入房间，A、B 用户均在 12:40 时离开房间，则语音时长合计为50分钟（A 用户40分钟，B 用户10分钟）。

## 语音消息及转文本服务
语音消息及转文本服务按语音消息 DAU 计费。

### 价格表

<table>
   <tr>
      <td>价格模型</td>
      <td>转文本支持语言</td>
      <td>Unit Price (USD/DAU/day)</td>
   </tr>
   <tr>
      <td  rowspan="2">按语音消息 DAU 计费</td>
      <td >仅简体中文、英文</td>
      <td>0.0019 </td>
   </tr>
   <tr>
      <td >全语种</td>
      <td>0.078 </td>
   </tr>
   </tr>
</table>



>!应用内用户收发语音消息即算作语音消息 DAU，语音消息 DAU 按照 openID 去重计算（openID 是应用内用户的唯一标识符，一个用户对应一个 openID）。



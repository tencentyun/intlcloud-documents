## 计费方式

解锁相应的音视频终端SDK功能，购买对应License资源所需支付的费用。

>! 功能与License的对应详情请参见 [SDK 下载](https://www.tencentcloud.com/document/product/647/34615)。

<table>
<thead>
<tr>
<th colspan="2" width="40%">计费项</th>
<th>计费说明</th>
<th width="22%">付费方式</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="4">腾讯云音视频终端SDK License 费用</td>
<td>直播推流 License</td>
<td>解锁<b>直播推流 + 视频播放</b>功能模块的授权。</td>
<td><ul style="margin:0">
<li><a href="#live_license">独立购买直播推流 License</a><br></li></td>
</tr>
<tr>
<td>短视频 License</td>
<td>解锁<b>短视频制作 + 视频播放</b>功能模块的授权。</td>
<td><ul style="margin:0">
<li><a href="#ugsv_license">独立购买短视频 License</a><br></li></td>
</tr>
<tr>
<td>视频播放 License</td>
<td>解锁<b>视频播放</b>功能模块的授权。</td>
<td><ul style="margin:0">
<li><a href="#play_license">购买视频播放 License</a></li></td>
</tr>
</tbody></table>

通过音视频终端SDK使用云服务时将产生的相应费用。

<table>
<thead>
<tr>
<th colspan="2" width="40%">计费项</th>
<th>计费说明</th>
<th width="22%">付费方式</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="4">音视频云服务费用</td>
<td>云直播服务（CSS）服务费用</td>
<td>使用云直播服务（CSS），配合音视频终端SDK 直播推流/播放功能模块快速将直播流推送到云端进行处理和分发，需收取相应的费用。</td>
<td><a href="https://www.tencentcloud.com/document/product/267/2819">云直播价格总览</a></td>
</tr>
<tr>
<td>实时音视频服务（TRTC）服务费用</td>
<td>音视频终端SDK业务需使用音视频语音通话、语聊房、视频/语音通话等音视频通信场景和互动直播连麦相关的实时音视频服务（TRTC）功能，需收取相应的费用。</td>
<td><a href="https://www.tencentcloud.com/document/product/647/34610">实时音视频价格总览</a></td>
</tr>
<tr>
<td>云点播服务（VOD）服务费用</td>
<td>音视频终端SDK业务涉及云点播服务（VOD），如直播内容录制并提供回放能力和短视频编辑、存储及分发播放，需收取相应的费用。</td>
<td><a href="https://www.tencentcloud.com/document/product/266/2838">云点播价格总览</a></td>
</tr>
<tr>
<td>即时通信服务（IM）服务费用</td>
<td>音视频终端SDK业务涉及即时通信（IM）产品，如房间管理、弹幕评论、红包送礼、直播连麦房间管理等功能，需收取相应的费用。</td>
<td><a href="https://www.tencentcloud.com/document/product/1047/34349">即时通信价格总览</a></td>
</tr>
</tbody></table>

[](id:license)

## 音视频终端SDK License

### 基础服务费用

音视频终端 SDK通过 License 来管理需要授权解锁的功能模块，目前直播推流、短视频和视频播放功能模块需要 License 来进行解锁，包含**直播推流 License**、**短视频 License**（**短视频 License 包括轻量版和标准版**）和**视频播放 License**。

- 直播推流 License 可用于开启**直播推流和视频播放**功能模块。
- 短视频 License 可用于开启**短视频制作和视频播放**功能模块。
- 视频播放 License 可用于开启**视频播放**功能模块。

提供两种计费方式，可以**通过购买相应云服务的资源包获取赠送的**直播 License 或者短视频 License 的 1 年有效期（**自资源包购买之日起计算，授权有效期为 1 年后到期次日 00:00:00 止**），也可以**购买独立**直播 License、短视频 License 或视频播放 License（**自绑定包名起计算，授权有效期为 1 年后到期次日 00:00:00 止**）。

>! 视频播放 License 授权解锁在音视频终端 SDK 10.1 版本（2022 年 05 月底）后上线。

#### 直播推流 License 计费价格[](id:live_license)

<table>
<thead>
<tr>
<th>直播推流 License 类型</th>
<th>有效期</th>
<th>解锁的功能模块</th>
<th>价格（美元）</th>
<th>获取方式</th>
</tr>
</thead>
<tbody><tr>
<td>直播 License <br>（<b>测试</b>）</td>
<td>28天</td>
<td rowspan=2>直播推流 + 视频播放</td>
<td>0</td>
<td><a href="https://">免费申请</a></td>
</tr>
<tr>
<td >直播推流 License</td>
<td >1年</td>
<td>5,988</td>
<td r><a href="https://buy.tencentcloud.com/license">立即购买</a></td>
</tbody></table>



#### 短视频 License 计费价格[](id:ugsv_license)

<table>
<thead>
<tr>
<th>短视频 License 类型</th>
<th>有效期</th>
<th>解锁的功能模块</th>
<th>价格（美元）</th>
<th>获取方式</th>
</tr>
</thead>
<tbody><tr>
<td>短视频标准版 License <br>（<strong>测试</strong>）</td>
<td>28天</td>
<td>短视频制作（标准版） + 视频播放</td>
<td>0</td>
<td><a href="https://console">免费申请</a></td>
</tr>
<tr>
<td>短视频轻量版 License</td>
<td>1年</td>
<td>短视频制作（轻量版） + 视频播放</td>
<td>1,899</td>
<td rowspan=3><a href="https://buy.tencentcloud.com/license">立即购买</a></td>
</tr>
<tr>
</tr>
<tr>
<td rowspan=2>短视频标准版 License</td>
<td rowspan=2>1年</td>
<td rowspan=2>短视频制作（标准版） + 视频播放</td>
<td>9,999</td>
</tr>
</tbody></table>

>? 短视频基础版 License 在精简版基础上增加滤镜、特效和转场等能力，快速轻松实现基于移动端的短视频应用，详情可参见 [短视频 License 功能详情](https://www.tencentcloud.com/document/product/1069/37914)。

#### 视频播放 License 计费价格[](id:play_license)

音视频终端 SDK（音视频终端SDK）移动端（Android & iOS & Flutter）即将发布 10.1 版本（2022 年 05 月底上线），10.1 版本起开始增加对**视频播放**功能模块的授权校验：

- **如果您的 App 已经拥有直播 License （原直播推流 License）或短视频 License 授权，当您升级至 10.1 版本后仍可继续正常使用**，不受到此次变更影响。
- 如果您此前未获得过直播 License （原直播推流 License）或短视频 License 授权，**且需使用新版本 SDK 中的直播播放或点播播放功能，则需购买指定 License 获得授权**，详情参见 [授权说明](#warrant)。
- 若您无需使用相关功能或未升级至最新版本 SDK，将不受到此次变更的影响。

<table>
<thead>
<tr>
<th width=15%>视频播放 License 类型</th>
<th>有效期</th>
<th>解锁的功能模块</th>
<th width=10%>价格<br>（美元）</th>
<th>获取方式</th>
</tr>
</thead>
<tbody><tr>
<td>测试版</td>
<td>28天</td>
<td rowspan=2>视频播放</td>
<td rowspan=2>0</td>
<td rowspan=2><a href="">免费申请</a></td>
</tr>
<tr>
<td>正式版</td>
<td>1年</td>
</tr>
</tbody></table>

[](id:warrant)

#### 授权说明

10.1 版本（2022 年 05 月底上线）后，直播 License（原直播推流 License）、短视频 License 和视频播放 License **均可**授权解锁新版本 SDK 的**视频播放**功能模块，您只需购买其中的**任意一种** License，即可正常使用新版 SDK 中的直播和点播播放功能。各 License 授权解锁详情如下：

<table>
<thead>
<tr>
<th rowspan="2" width=20%>License 类型</th>
<th colspan="3">解锁的功能模块授权</th>
<th rowspan="2">License 获取方式</th>
</tr><tr>
<th>直播推流</th>
<th>短视频制作</th>
<th>视频播放</th>
</tr>
</thead>
<tbody>
<tr>
<td>直播推流 License</td>
<td>&#10003; </td>
<td>-</td>
<td>&#10003; </td>
<td><ul style="margin:0">
<li>购买独立直播 License 一年使用授权</li></ul></td>
</tr>
<tr>
<td>短视频 License</td>
<td>-</td>
<td>&#10003; </td>
<td>&#10003; </td>
<td><ul style="margin:0">
<li>购买独立短视频 License 一年使用授权</li></ul></td>
</tr>
<tr>
<td>视频播放 License</td>
<td>-</td>
<td>-</td>
<td>&#10003; </td>
<td><ul style="margin:0">
<li>免费获取视频播放 License 一年使用授权</li></ul></td>
</tr>
</tbody></table>

#### 计费说明

- 每个腾讯云账号可分别**免费申请 1 次**直播 License 、短视频 License、视频播放 License 进行测试体验产品功能，首次申请会先提供 14 天有效期，可在控制台中再续期 14 天，共计 28 天。
- 音视频终端SDK License 可以用于绑定新的包名，或者替换已经绑定包名的音视频终端SDK License，替换后该包名更新为新音视频终端SDK License 的有效期，原绑定的音视频终端SDK License 被替换后为未绑定状态，有效期不变。
- 有效期说明：
  - 资源包：购买资源包赠送的音视频终端SDK License 有效期 1 年**自资源包购买之日起计算**，1 年后到期次日的 00:00:00 止。流量包用尽不影响绑定的 License 使用，可通过换绑资源包来实现 License 的续期。
  - 独立 License：购买后，独立的音视频终端SDK License 为未激活状态。独立音视频终端SDK License 绑定包名后激活有效期。**自绑定包名起计算**，授权有效期为 1 年后到期次日 00:00:00 止。
- **每个音视频终端SDK License 可以绑定一个 iOS 包名（Bundle ID）和一个 Android 包名（Package Name），不区分业务环境**。若有多个包名需要接入，需购买对应数量的音视频终端SDK License 进行绑定。

- **购买云服务资源包赠送的音视频终端SDK License 不支持单独退款，绑定包名后即视为音视频终端SDK License 已使用，对应资源包亦不支持 5 天无理由退款。**
- **购买的独立音视频终端SDK License 绑定包名激活有效期后不支持退款。**

>! 若资源包已使用或购买已超过 5 天自然日，不论是否用尽均不支持退款。


### 增值服务费用

[](id:value)

**除了音视频终端SDK License 外，在您使用音视频终端SDK 的过程中，还可能产生以下产品的费用，请您根据实际使用情况进行使用和选购。**

## 云直播服务（CSS）

腾讯音视频终端 SDK提供的终端的直播推流/播放功能模块，需要对应有后台能够接收、处理和分发直播流，推荐您使用 [腾讯云直播](https://www.tencentcloud.com/products/css) 服务，可以配合直播推流模块快速将直播流推送到云端进行处理和分发。

云直播提供的相关能力包括了直播接流、云端录制、实时转码、实时截图、直播播放分发等一系列直播配套功能服务，对应的计费包括：

- 基础服务费用：正常直播推流接流和直播播放产生的消耗，按照流量/带宽计费。
- 增值服务费用：包括直播转码（含混流和水印）、直播录制、实时截图、新版直播连麦和拉流转推等增值服务产生的用量消耗。

>? 更多费用相关说明，请参见 [云直播价格总览](https://www.tencentcloud.com/document/product/267/2819)。


## 实时音视频服务（TRTC）

若您的音视频终端SDK 业务需要使用音视频语音通话、语聊房、视频/语音通话等音视频通信场景的功能，推荐您使用 [实时音视频](https://www.tencentcloud.com/products/trtc)服务。或者您有互动直播连麦相关的需求，也可以通过实时音视频实现。

实时音视频的计费主要包括：

- 基础服务根据具体应用场景可细分为语音互动直播、视频互动直播、语音通话和视频通话四种，按对应使用时长计费。
- 增值服务指的是基于四种基础服务之上额外提供的增值功能，包括云端录制、云端混流转码等。

>? 更多费用相关说明，请参见 [实时音视频价格总览](https://www.tencentcloud.com/document/product/647/34610)。

## 云点播服务（VOD）

如果您希望您的音视频终端SDK 业务将直播内容录制并提供回放能力，那就需要在直播录制前开启云点播服务。或者您在使用短视频编辑后，需要存储视频和对视频进行分发播放，可以使用 [云点播](https://www.tencentcloud.com/products/vod) 服务。

云点播产品的计费主要包括：

- 视频存储：上传到云点播服务的视频源文件和转码后的视频文件占用的存储空间，按存储容量计费。
- 视频转码：存储在云点播服务的视频源文件进行转码处理时，按目标文件的规格和时长计费。
- 播放分发加速：视频进行播放时，使用云点播分发加速产生的费用，按下行流量计费。

>? 更多费用相关说明，请参见 [云点播价格总览](https://www.tencentcloud.com/document/product/266/2838)。

## 即时通信服务（IM）

当您的音视频终端 SDK（音视频终端SDK）业务包括房间管理、弹幕评论、红包送礼、直播连麦房间管理等功能时，推荐您使用 [即时通信 IM](https://www.tencentcloud.com/products/im) 服务。更多信息请参见 [即时通信价格总览](https://www.tencentcloud.com/document/product/1047/34349)。

>!
>- 连麦房间即为 IM 服务的直播群（AvChatRoom），可购买不同版本套餐包，或直接购买额外的增值服务扩展连麦房间的创建上限。
>- 借助腾讯云即时通信 IM 服务可以实现包括：弹幕评论、聊天、发红包及送礼等互动功能。您也可以通过自己开发或第三方服务等方式实现以上功能。
>- 即时通信 IM 提供了免费的体验版可用于测试，您可根据实际业务需要选购和开通对应的版本功能和功能包。

音视频终端 License包括**直播推流 License**、**短视频 License**、**视频播放 License**，计费购买详情请参见 [价格总览](https://www.tencentcloud.com/document/product/647/50553)。购买后可在[实时音视频](https://console.tencentcloud.com/trtc)、 [云直播](https://console.tencentcloud.com/live/license) 或 [云点播](https://console.tencentcloud.com/vod/license)任何一个产品的控制台 对各 License 进行 新增和续期 等操作。各 License 解锁相关功能模块如下：

| 音视频终端 License | 解锁功能模块            |
| -------------------- | ----------------------- |
| 直播推流 License     | 直播推流 + 视频播放 |
| 短视频 License       | 短视频（轻量版/标准版） + 视频播放 |
| 视频播放 License | 视频播放 |

>! 10.1 版本起，直播推流 License 和短视频 License 包含了视频播放 License 全部能力，因此也可用于解锁播放器 SDK 的视频播放功能。

音视频终端 SDK 下的直播推流 License、短视频 License、视频播放 License ，**本文档将以直播推流 License 为例**，对音视频终端 License 测试版和正式版的新增与续期等操作进行说明指引。

[](id:test)
## 测试版 License

[](id:creat_test)
### 申请测试版 License

您可以免费申请直播模块的测试版 License（免费测试有效期为28天）体验测试。

>? 当申请测试开始时间为  `2022-10-1 11:34:55` ，则28天后到期时间为  `2022-10-28 00:00:00` 。


申请测试模块时，您可以选择**新建测试 License 并申请测试功能模块**或在**已创建的测试应用中申请测试新功能模块**两种方式创建测试 License。
<dx-tabs>
::: 方式一：新建测试 License 并申请测试功能模块
1. 登录 [实时音视频](https://console.tencentcloud.com/trtc)、[云直播](https://console.tencentcloud.com/live/license) 或 [云点播](https://console.tencentcloud.com/vod/license)任何一个产品的控制台，单击**新建测试 License**。
![](https://qcloudimg.tencent-cloud.cn/raw/4507bd038c2a6e43cf91205383a1904f.png)
2. 根据实际需求填写 `App Name`、`Package Name` 和 `Bundle ID`，勾选功能模块 **直播**（直播推流 + 视频播放），单击创建。
<img src="https://qcloudimg.tencent-cloud.cn/raw/af9ee37d5d25af0dc63221ff13cac3d6.png" style="zoom:67%;" />
1. 测试版 License 成功创建后，页面会显示生成的 License 信息。**在 SDK 初始化配置时需要传入 Key 和 License URL 两个参数，请妥善保存以下信息。**
![](https://qcloudimg.tencent-cloud.cn/raw/67b33614792136bb295b3f47a024291f.png)
:::
::: 方法二：已创建的测试应用中申请测试新功能模块
若您想在已创建的测试应用中申请**直播推流**（直播推流 + 视频播放）功能测试模块，步骤如下：
1. 选择您想测试的应用，单击**测试新功能模块**。
![](https://qcloudimg.tencent-cloud.cn/raw/026830658f7815b3d43432a501f2327a.png)
2. 勾选功能模块 **直播推流**（直播推流 + 视频播放），单击**确定**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/80d4dffff43aa6e299088d4a1b06db72.png" style="zoom:67%;" />
:::
</dx-tabs>

>? 
>- 测试版 License 有效期内可单击右侧的 **编辑**，进入修改 Bundle ID 和 Package Name 信息，单击 **确定** 即可保存。
>- 若无 Package Name 或 Bundle Id，可填写“-”。
>- 测试版 License 有效期共28天，**只能申请一次**。若您需继续使用，请购买 [正式版 License](#formal)。

[](id:up_test)
### 升级测试版 License
若您需要将直播功能模块的测试版 License 升级成为正式版 License，获得一年的有效期使用期。具体操作如下：
1. 单击测试版 License 直播功能模块中的 **升级**。
![](https://qcloudimg.tencent-cloud.cn/raw/6daf850b30a29014ab8cbd0f1a3f500f.png)
2. 进入升级功能模块界面，点击**立即绑定** ，选择需要绑定的云直播流量资源包或独立 License（若没有可绑定的 License 资源，可前往 [音视频终端SDK 购买页](https://buy.tencentcloud.com/license) 购买），单击 **确定** 即可升级到直播功能模块的正式版 License。
<img src="https://qcloudimg.tencent-cloud.cn/raw/087fb89a73fa9cffd80e0da4840783f6.png" alt="image" style="zoom: 50%;" /><img src="https://qcloudimg.tencent-cloud.cn/raw/1ff7b009cbce37598521d43df2cdae61.png" style="zoom:50%;" />

[](id:formal)

## 正式版 License
[](id:creat_formal)
### 购买正式版 License
1. 购买方式：
    - [**购买**](https://buy.tencentcloud.com/license) 独立 [直播推流 License](https://www.tencentcloud.com/document/product/647/50553) 获得使用授权（自绑定包名之日起计算，授权有效期为1年后到期次日00:00:00止）。
2. 绑定直播正式版 License。您可以选择**新建正式应用并绑定 License**或在**已创建的应用上解锁直播正式版模块并绑定 License**两种方式进行正式版 License 绑定 。
<dx-tabs>
::: 方式一：新建正式应用并绑定 License
1. 进入[实时音视频](https://console.tencentcloud.com/trtc)、 [云直播](https://console.tencentcloud.com/live/license) 或 [云点播](https://console.tencentcloud.com/vod/license)任何一个产品控制台 License管理，单击**新建正式 License**。
![](https://qcloudimg.tencent-cloud.cn/raw/c7689b0f319f616a5e5e3ecf47267b65.png)
2. 填写正式应用的 `App Name`、`Package Name` 和 `Bundle ID` 信息，勾选功能模块**直播**（直播推流 + 视频播放），单击**下一步**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f0ba8765431755c7807787782a157297.png" style="zoom:67%;" />
3. 进入选择资源项并绑定 License 界面，点击**立即绑定** ，选择**未绑定**的直播流量资源包或独立 License（若没有可绑定的 License 资源，可前往 [音视频终端 SDK 购买页](https://buy.tencentcloud.com/license) 购买），并单击**确定**即可创建应用并生成正式版 License。
<img src="https://qcloudimg.tencent-cloud.cn/raw/7ddb304e3d9e35959c0ba93a4138189a.png" style="zoom:50%;" />

>? 单击**确定**前需要再次确认 Bundle ID 和 Package Name 与业务使用包名信息一致，如与提交到商店的不一致，请在提交前进行修改，**正式版 License 一旦提交成功将无法再修改 License 信息**。

4. 正式版 License 成功创建后，页面会显示生成的正式版 License 信息。在 SDK 初始化配置时需要传入 Key 和 License URL 两个参数，请妥善保存以下信息。
![](https://qcloudimg.tencent-cloud.cn/raw/11fcae56bf1fcad8641ba789bdaaa517.png)
:::
::: 方式二：已创建的正式版应用中解锁模块
1. 选择您需要增加**直播推流**（直播推流 + 视频播放）功能模块的正式应用，单击**解锁新功能模块**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/e1ab736ce2f80e74214dbca9a47f10fd.png" style="zoom:67%;" />
2. 选择**直播推流**（直播推流 + 视频播放），单击**下一步**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/1ff7b009cbce37598521d43df2cdae61.png" style="zoom: 67%;" />
3. 进入选择资源项并绑定 License 界面，点击**立即绑定** ，选择**未绑定**的直播流量资源包或独立 License（若没有可绑定的 License 资源，可前往 [音视频终端 SDK 购买页](https://buy.tencentcloud.com/license) 购买），并单击**确定**即可在应用下生成正式版直播功能模块。
<img src="https://qcloudimg.tencent-cloud.cn/raw/095e35fc6947c3399ca30d66d019b2f5.png" style="zoom:67%;" />
:::
</dx-tabs>

[](id:update_formal)
### 更新正式版 License 有效期
您可以登录[实时音视频](https://console.tencentcloud.com/trtc)、 [云直播](https://console.tencentcloud.com/live/license) 或 [云点播](https://console.tencentcloud.com/vod/license)任何一个产品控制台 License管理 页面查看直播正式版 License 的有效期，也可通过在 [消息订阅](https://console.cloud.tencent.com/message/subscription) 中订阅音视频终端 SDK，配置**站内信**/**邮件**/**短信**/**微信**/**企微**等消息接收渠道，接收正式版 License 到期提醒。直播推流正式版 License 将在到期时间距离当前时间为30天、15天、7天、1天时各向您发送一次到期提醒，提示您及时续费以免影响正常业务运行。若您的直播推流正式版 License 已到期，可进行如下操作进行续期：
1. 选择您需要更新有效期的 License，单击直播功能模块内的 **更新有效期**。
![](https://qcloudimg.tencent-cloud.cn/raw/534f5d02cb72a6950ad5d37fb3666c70.png)
2. 单击**立即绑定** ，选择**未绑定**的直播流量资源包或独立 License（若没有可绑定的 License 资源，可前往 [音视频终端 SDK 购买页](https://buy.tencentcloud.com/license) 购买），单击**确定**即可。
<img src="https://qcloudimg.tencent-cloud.cn/raw/6b1f279e5cd439386147c4f4aa96d852.png" style="zoom:50%;" />
3. 查看更新后的有效期情况。

>! **正式版直播推流 License 不支持信息修改**，若您需要修改 License 信息，购买资源包后请勿用于 License 有效期的更新，请单击 **新增 License** 重新新增 License 绑定新的包名信息。
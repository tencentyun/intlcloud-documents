### 关于 License 版本问题？

短视频 SDK 分基础版和企业版，从4.5版本开始需要 License，基础版只需要短视频的 License（TXUgcSDK.licence），企业版还同时需要 Pitu 的 License（YTFaceSDK.licence），把 License 放到工程目录，并修改为对应的名字即可。

4.9版本开始 License 使用方式有改变，可以选择是否把 License 打包到项目中。使用时需要调用 setLicenceURL：key：接口设置 License 的 url 和 key。

>! 4.5 - 4.7版本的 SDK 不支持 License 自动续期，4.9版本开始才支持自动续期。4.9的 SDK 可以兼容之前的 Licence（url 和 key 不能传 null，可以随便传个字符串），但是新的 License 无法在4.9之前的 SDK 上使用。



### 测试 License 到期后是否可以延期？

您可以免费申请测试版 License（免费测试有效期为14天，可续期1次，共28天）体验测试。到期后请尽快购买正式license，详情可提交工单咨询或[联系商务](https://intl.cloud.tencent.com/contact-us)。


>! 试用期内申请测试续期，则续期到期时间以申请测试时刻为准；若试用期结束后申请测试续期，则续期到期时间以申请测试续期时刻为准。
>- 当申请测试开始时间为 `2021-08-12 10:28:41`，则14天后到期时间为 `2021-08-26 10:28:41`。
>- 免费续期一次时，若在试用期14天内申请续期，则到期时间为 `2021-09-09 10:28:41`；若在试用期14天结束后申请续期，申请续期的时间为 `2021-08-30 22:26:20`，则续期的到期时间为 `2021-09-13 22:26:20`。



### 测试 License 能否更改 Android 的 PackageName 和 iOS 的 BundleID?

测试 License 支持更改，在 [云点播控制台](https://console.cloud.tencent.com/vod/license/video) 选择测试 License 信息右上角，单击【编辑】即可进行修改。


### License 可以同时支持多个 App 吗？

一个 License 只能对应一个 PackageName 和 BundleID，不支持多个 App。


### License 应该如何确认绑定关系（Android 的 PackageName 和 iOS 的 BundleID）?

在填写时用户需要确认绑定正式上架 App Store 的 iOS 所对应的 Bundle ID 和正式上架应用市场 Android 的 Package Name。



### License 校验失败，如何排查？

建议您可以参考以下几点进行排查：

- 确认您的 License 是否在有效期内。
- 确认 License 信息里的 Package Name 是否与项目里面的包名一致。
- 确认 License 中的 LicenseUrl 协议是否为 HTTPS。

>? 若上述方法无法解决您的问题，建议**卸载应用重新安**装或 [提工单](https://console.cloud.tencent.com/workorder/category) 解决。



### 没有 bundleid，Android 端是不是无法使用 License？

bundleid 类似于 Android 端的 package name，若您不集成 iOS 端，可随意填写，不使用即可。


### 个人购买的短视频 SDK License 可以用于企业吗？

短视频 SDK 暂仅支持购买所在账号进行使用，暂无个人实名认证以及企业实名认证的限制。

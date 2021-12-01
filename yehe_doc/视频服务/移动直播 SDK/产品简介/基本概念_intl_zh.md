### 推流

主播将本地视频源和音频源推送到腾讯视频云服务器，在有些场景中也被称为“RTMP 发布”。

### 拉流

即直播播放，指已实现直播推流之后，用指定地址将腾讯视频云服务器中的视频源和音频源拉取播放的过程。其视频源是实时生成的，有人推流直播才有意义，一旦主播停播，直播 URL 也就失效了。而且由于是实时直播，所以播放器在播直播视频的时候是没有进度条的。

### 推流域名

指用于推送直播流的域名，必选配置，该域名必须在使用直播服务前完成注册并备案。配置完推流域名后，直播服务会生成对应的推流地址，拼接规则请参见 [自主拼装推流 URL](https://intl.cloud.tencent.com/document/product/1071/39359)。

### 播放域名

指用于播放直播流的域名，必选配置，该域名必须在使用直播服务前完成注册并备案。配置完播放域名后，直播服务会生成对应的播放地址，拼接规则请参见 [自主拼装播放 URL](https://intl.cloud.tencent.com/document/product/1071/39359)。

### UserSig

UserSig（用户签名）是腾讯云设计的一种安全保护签名，用于对一个用户进行登录鉴权认证，确认用户是否真实，阻止恶意攻击者盗用您的云服务使用权。详情请参见 [生成 UserSig 签名](https://intl.cloud.tencent.com/document/product/1071/39471) 文档。

### License

移动直播支持两个版本的 SDK License，分别是测试版和国际版，具体获取方式请参见 [体验与购买 License](https://intl.cloud.tencent.com/document/product/1071/38546) 。通过 License 可开启对应的移动直播 SDK 功能服务，具体功能说明请参见 [SDK 功能列表](https://intl.cloud.tencent.com/document/product/1071/38149) 。

### 录制回看

录制回看功能依托于腾讯云的**云点播服务**支撑，需要先在腾讯云的管理控制台 [开通云点播服务](https://console.cloud.tencent.com/vod)，并在云直播控制台中完成域名 [录制配置](https://intl.cloud.tencent.com/document/product/267/31074)，直播推流完成后录制生成的文件可前往云点播控制台的【媒资管理】[查看视频](https://intl.cloud.tencent.com/document/product/266/33895)。


### 快直播
快直播（Live Event Broadcasting，LEB）是标准直播在超低延迟播放场景下的延伸，比传统直播协议延迟更低，为观众提供毫秒级的极致直播观看体验。 能够满足一些对延迟性能要求更高的特定场景需求，例如在线教育、体育赛事直播、在线答题等。

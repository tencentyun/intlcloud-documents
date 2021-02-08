[](id:que1)
### 移动直播 License 是必须购买的吗？
移动直播 SDK 的直播推流功能，必须通过购买移动直播 License 进行解锁。
>! 短视频 License 无法解锁移动直播相关功能。


[](id:que2)
### 移动直播 License 有单独购买入口吗？
不支持单独购买。
- 移动直播基础版和企业版 SDK License：需 [联系腾讯云商务](https://intl.cloud.tencent.com/contact-sales) 申请。

[](id:que3)
### 移动直播基础版 License 和移动直播企业版 License 有什么区别？
移动直播基础版 License 即可解锁直播推流和播放功能，以及基础的美颜功能（美白、磨皮等）。
移动直播企业版 License 是在其之上，增加了高级美颜（大眼、瘦脸）、绿幕功能、动效贴纸、AI 抠图等能力，还可以配合美妆和手势素材实现额外的功能。

>?
>- SDK 下载中的3个版本的 SDK 均可用移动直播基础版 License 来解锁直播推流和播放功能。
>- 企业版中的高级美颜相关功能只能通过移动直播企业版 License 来解锁。


[](id:que4)
### 一个账号下能创建多个 License 吗？
同一个账号下创建 License 的数量没有限制。为了方便用户管理，相同包名的 License 建议通过续期的方式延长有效时间。

[](id:que5)
### 相同包名可以创建多个 License 吗？
可以，多个 License 填写相同的包名不会影响使用，不过同时创建多个 License 有效期会各自计算，一般不建议创建多个相同包名的 License。

[](id:que6)
### License 可以修改吗？
移动直播 License 可通过续期来延长有效时间，包名信息不支持修改，请您在添加 License 先核对包名在应用商店里是否被占用，提交后不支持修改和替换。

[](id:que7)
### 为什么我创建了多个 License ，但是 licenseurl 和 key 都是一样的？
同一个账号下移动直播的 licenseurl 和 key 默认是相同的。这样保证了测试 License 、正式 License、不同包名的 License 均可以复用相同的接口信息。

>?不建议使用免费测试的 License 发布到线上运行。您可以通过添加新的正式版 License，即可无需再修改接口中的 licenseurl 和 key，切换到正式版 License。



在使用 License 的过程中，您可能会遇见以下问题，可以参考本文的解答。

[](id:q1)

### License、License Key和腾讯特效SDK有什么关系？

您需要获得腾讯授予的License从而合法地使用腾讯特效SDK。License为您在试用或购买 SDK 之前需要获得的许可。若未经License授权的产品使用将构成侵权。您可以获得两种类型的License，测试License和正式License。

SDK 是为了更好的使用整个服务所特定的软件包、软件框架、操作系统等建立应用软件时的开发工具集合。一旦您从腾讯获得使用 SDK 的License，您将获取到一对License Key和License  URL信息。您必须要将生效授权License Key和 LicenseURL 并填入到 SDK 中相应位置，方能启用腾讯特效功能。

[](id:q2)

### 如何获取腾讯特效正式版 License？

若您需要在您的业务中使用腾讯特效 SDK 功能，您可参见计费概述，根据您的需求选择 SDK 套餐进行购买。通过购买相应的SDK 套餐获取 License 解锁授权，成功购买套餐包以后，在腾讯特效SDK控制台进行绑定，使用相应的功能。具体操作请参见 [购买正式版 License](https://www.tencentcloud.com/document/product/1143/50266#.E8.B4.AD.E4.B9.B0.E6.AD.A3.E5.BC.8F.E7.89.88-license)。

[](id:q3)

### License 的有效期是多长？过期后如何更新 License？

- **测试版 License**：的有效期是审批通过后，从签发 License 之日开始往后计算一个月（28天）的时长。比如您在2022年01月01日申请了测试版 License，2022年01月02日申请通过审批并自动签发了 License，测试版 License 将在2022年01月31日的00:00:00过期。
- **正式版 License**：的有效期是从绑定 License 之日开始往后计算一年（365天）的时长。比如您在2022年01月01日绑定了正式版 License，正式版 License 将在2023年01月02日的00:00:00过期。
- 正式版 License 过期后需要重新购买新的 License 进行续期，正式版 License 续期指引，请参见 [续期正式 License](https://www.tencentcloud.com/document/product/1143/50266#.E6.9B.B4.E6.96.B0.E6.AD.A3.E5.BC.8F.E7.89.88-license-.E6.9C.89.E6.95.88.E6.9C.9F)。

[](id:q4)

### 签发后的 License 支持修改包名吗？

测试版 License 能更改 Android 的 Package Name 和 iOS 的 Bundle ID。

正式版 License 一旦添加绑定后，是不支持更改 Package Name 和 Bundle ID。

[](id:q5)

### License 支持的包名个数是多少？授权台数是多少？

每添加一个 License 会支持 Bundle ID 和 Package Name 两个不同的包名，整个账号可以添加的 License 数量是没有限制的。目前 License 对授权终端的台数也是没有限制的。

[](id:q6)

### 腾讯特效 SDK 如何升降级？

腾讯特效 SDK 一共提供了 14 个版本，各版本功能差异请参见 [计费概述](https://intl.cloud.tencent.com/document/product/1143/45371)。您可以在正式版 License 到期之后，选择购买切换为更符合您场景需求的版本。当前 License 仍在有效期内时，我们不支持 SDK 的升降级切换。

测试版 License 是统一签发的套餐最高级版本 S1 - 04 的授权，您可以测试 SDK 的全功能。测试期结束前，您可以更换为与您使用场景匹配的正式版 SDK 和 License。
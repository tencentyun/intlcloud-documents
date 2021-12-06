## 测试版 License

### 申请测试版 License

您可以免费申请国际版 License（免费测试有效期为14天，可续期1次，共28天）体验测试。

>! 试用期内申请测试续期，则续期到期时间以申请测试时刻为准；若试用期结束后申请测试续期，则续期到期时间以申请测试续期时刻为准。
> - 当申请测试开始时间为 `2021-08-12 10:28:41`，则14天后到期时间为 `2021-08-26 10:28:41`。
> - 免费续期一次时，若在试用期14天内申请续期，则到期时间为 `2021-09-09 10:28:41`；若在试用期14天结束后申请续期，申请续期的时间为 `2021-08-30 22:26:20`，则续期的到期时间为 `2021-09-13 22:26:20`。

具体步骤如下：

1.  登录云直播控制台，在左侧菜单中选择 **直播 SDK** > **[License 管理](https://console.intl.cloud.tencent.com/live/license)**，单击 **Get License**。

   ![](https://qcloudimg.tencent-cloud.cn/raw/49e40218bbe80536940e5fb313450860.png)

2. 根据实际需求填写 `Application Name`、`Package Name` 和 `Bundle ID`，单击 **Confirm**。

   ![](https://qcloudimg.tencent-cloud.cn/raw/680f5ac056286d90e10b03e931252d59.png)

3. 测试版 License 成功创建后，页面会显示生成的 License 信息。在 SDK 初始化配置时需要传入 Key 和 License URL 两个参数，请妥善保存以下信息。

   ![](https://qcloudimg.tencent-cloud.cn/raw/e22b61bc11e73c7ea57bdc58df527046.png)

>?
>- 测试版 License 有效期内可单击右侧的 **Edit**，进入修改 Bundle ID 和 Package Name 信息，单击 **Confirm** 即可保存。
>- 若无 Package Name 或 Bundle Id，可填写“-”。

### 续期测试版 License

测试版 License 初次申请默认有效期默认为14天，期满后您可续期 **1次**。单击测试版 License 模块右侧的 **Edit**，进入修改界面，单击 **Confirm** 重新保存即可续期14天。

![](https://qcloudimg.tencent-cloud.cn/raw/a693874fc6d0d658170913beaef8bd2f.png)

如图所示，有效期已更新：

![](https://qcloudimg.tencent-cloud.cn/raw/cd5f234437e6facf4157401a0d98af98.png)

>?  测试版 License 有效期共28天，**只能续期一次**。若您需继续使用，请购买 [正式版 License](https://intl.cloud.tencent.com/document/product/1071/38546#.E6.AD.A3.E5.BC.8F.E7.89.88-license)。

## 正式版 License

### 购买正式版 License

1. [购买移动直播 SDK 国际版 License](https://buy.intl.cloud.tencent.com/mlvb)，获得正式的国际版 License 一年使用授权（有效期至到期次日的00:00:00止），计费价格请参见 [购买指南](https://intl.cloud.tencent.com/document/product/1071/38114)。

>?  例如，您在2021年12月01日 14:16:52 购买了正式的国际版 License 一年有效期，该 License 于2022年12月02日 00:00:00 到期。

2. 进入 **直播 SDK** > **[License 管理](https://console.intl.cloud.tencent.com/live/license)** ，单击 **Create** 按钮。填写 `App Name`、`Package Name` 和 `Bundle ID` ，完成后单击 **Confirm**。

   ![](https://qcloudimg.tencent-cloud.cn/raw/276281c94f5c6e53af157d480608bd12.png)

   >? 
   >- 单击 **确定** 前需要再次确认 Bundle ID 和 Package Name，如与提交到商店的不一致请提前进行修改，**一旦提交成功将无法再修改 License 信息**。
   >- **正式的国际版 License 不支持信息修改**，若您需要修改 License 信息，购买资源包后请勿用于续期 License，请单击 **Create** 重新创建 License 绑定新的包名信息。

3. 正式版 License 成功创建后，页面会显示生成的正式版 License 信息。在 SDK 初始化配置时需要传入 Key 和 License URL 两个参数，请妥善保存以下信息。

   ![](https://qcloudimg.tencent-cloud.cn/raw/7969480ebb9126eb0fbc5cb8f7ff4bc8.png)

### 更新正式版 License有效期

您可以登录 **直播 SDK**>**[License 管理](https://console.intl.cloud.tencent.com/live/license)** 页面查看国际版 License 的有效期，若您的国际版 License 已到期，可进行如下操作进行续期：

1. 选择您需要更新有效期的 License，单击 **Renew**。

   ![](https://qcloudimg.tencent-cloud.cn/raw/bbaf91140cf38c5dd3cafdbd8313b5b1.png)

2. 确认需要更新有效期的应用信息，选择需要更新有效期的时长，单击 **Renew** 跳转至购买页完成支付。

   ![](https://qcloudimg.tencent-cloud.cn/raw/cf7d6888853a6b234f989a40f4b77df9.png)

3. 查看更新后的有效期情况。

   >! **正式的国际版 License 不支持信息修改**，若您需要修改 License 信息，购买资源包后请勿用于续期 License，请单击 **Create** 重新创建 License 绑定新的包名信息。


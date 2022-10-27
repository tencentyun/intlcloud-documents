**腾讯特效SDK 提供美颜特效相关能力。申请免费测试 License 即可接入体验，最多可测试28天。**

[](id:test)
## 移动端测试 License

### 申请测试版 License[](id:create_test)

您可以免费申请腾讯特效模块的测试版 License（免费测试有效期为14天，可续期1次，共28天）体验测试。
测试版 License 您可根据自己的需求选择相应的能力进行申请。您可对美颜特效套餐以及原子能力的测试申请；其中套餐仅支持签发最高级版本 S1 - 04 的授权，您可以用此版本测试腾讯特效 SDK套餐全功能，最高级版本 S1 - 04 功能说明请参见 [功能说明](https://intl.cloud.tencent.com/document/product/1143/45376) 。套餐 S1-04 中包含了 X1-01 人像分割能力，其余能力不包含。

>!**腾讯特效功能模块在申请之后，需要审核通过才能签发授权**，测试版授权到期时间以审核通过时刻为准；若试用期结束后申请测试续期，则续期到期时间以申请测试续期时刻为准。
>- 当提交腾讯特效功能模块测试版审核信息后，进入**审核中状态**，审核时间通常 1-2 个工作日。提交审核信息时间为 `2022-05-24 12:47:33，审核通过时间为 `2022-05-24 15:23:46，则开始时间为 `2022-05-24 15:23:46，14天后到期时间为 `2022-06-09 00:00:00`。
>- 免费续期一次时，若在试用期14天内申请续期，则到期时间为 `2022-06-23 00:00:00；若在试用期14天结束后申请续期，申请续期的时间为 `2022-08-06 22:26:20，则续期的到期时间为 `2022-08-22 00:00:00。

申请测试模块。您可以选择**新建测试 License 并申请测试功能模块**或在**已创建的测试应用中申请测试新功能模块**两种方式创建测试 License。
<dx-tabs>
::: 方式一：新建测试 License 并申请测试功能模块

1. 登录 [**腾讯特效SDK控制台 > 移动端 License**](https://console.tencentcloud.com/xmagic)，单击**新建测试 License**。
![](https://qcloudimg.tencent-cloud.cn/raw/84f8ab5111e32c16ef6553b14ac72fd7.png)
2. 根据实际需求填写 `App Name`、`Package Name` 和 `Bundle ID`，选择所需测试的能力 **高级套餐 S1 - 04**、**原子能力X1-01**、**原子能力X1-02**，勾选后准确填写 **公司名称、所属行业类型**，上传**公司营业执照**，单击**确定**提交审核申请，等待人工审核流程。
<img src="https://qcloudimg.tencent-cloud.cn/raw/0d4f80aa8fd068a9d562ee5246a1e63a.png" style="zoom:50%;" />
3. 测试版 License 成功创建后，页面会显示生成的 License 信息。此时 Key 和 LicenseURL 两个参数暂未生效，需提交的审核通过后方才生效使用。**在 SDK 初始化配置时需要传入 Key 和 License URL 两个参数，请妥善保存以下信息。**
![](https://qcloudimg.tencent-cloud.cn/raw/d2bec2a1877a5b1ac83a4ae07e30db39.png)
> ?
> - 测试版 License 有效期内可单击右侧的**编辑**，进入修改 Bundle ID 和 Package Name 信息，单击**确定**即可保存，但会导致此测试 License 下生效中的测试版腾讯特效功能模块**重新进入审核流程**，待审核通过后方可继续使用。
>  ![](https://qcloudimg.tencent-cloud.cn/raw/733ce3011060a2c552435ebe7115d643.png)
> - 若无 Package Name 或 Bundle Id，可填写“-”。

:::
::: 方法二：已创建的测试应用中申请测试新功能模块
若您想在已创建的腾讯特效测试应用中申请新的功能测试模块，步骤如下：
1. 选择您想测试的应用，单击**测试新功能模块**。
![](https://qcloudimg.tencent-cloud.cn/raw/5ec68592f2bb1f24335b15d6bff1a384.png)
2. 勾选功能模块 **高级套餐 S1 - 04**/**原子能力X1-01**/**原子能力X1-02**，勾选后准确填写 **公司名称、所属行业类型**，上传**公司营业执照**，单击**确定**提交审核申请，等待人工审核流程。 
<img src="https://qcloudimg.tencent-cloud.cn/raw/7ee87ffbd3015d1ed31176bc48133595.png" style="zoom:80%;" />
:::
</dx-tabs>

3. 提交审核申请后模块进入**公司资质审核中**，审核时间通常 1-2 个工作日。可单击**查看审核信息**查看提交的审核信息。
![](https://qcloudimg.tencent-cloud.cn/raw/a27c350d9de411a9b629318703cbe2a4.png)
![](https://qcloudimg.tencent-cloud.cn/raw/4924c69299fa4d78ba7905a9111433af.png)
4. 审核通过后，腾讯特效功能模块状态为**正常**，腾讯特效测试版 License 申请成功，您可开始使用腾讯特效功能模块。
![](https://qcloudimg.tencent-cloud.cn/raw/f7e039ac73e24766cbaa240b98b06a4c.png)
>? **若审核失败**未通过，单击**审核结果**查看审核结果和审核备注，您可根据审核备注知悉审核失败原因，单击**重新发起审核**。更改审核信息并提交，等待人工审核流程。
>![](https://qcloudimg.tencent-cloud.cn/raw/7e2e93d6e4091fbcab1bf9c865868bd5.png)

[](id:renewal_test)
### 续期测试版 License
测试版 License 初次申请默认有效期默认为14天，期满后您可续期**1次**。单击功能模块**腾讯特效**右侧的**续期**，单击**确定续期**即可续期该功能模块14天。
![](https://qcloudimg.tencent-cloud.cn/raw/95f05996f1ae77f5b32fb051d3490c68.png)

>? 测试版 License 有效期共28天，**只能续期一次**。若您需继续使用，请购买 [正式版 License](#create_formal)。

[](id:upgrade_test)
### 升级测试版 License
若您需要将腾讯特效模块的测试版 License 升级成为正式版 License，增加使用的有效期，请先 [选择并购买腾讯特效正式版套餐包](https://buy.cloud.tencent.com/vcube?type=magic)，然后执行如下操作：
1. 单击测试版 License 腾讯特效模块中的**升级**。
![](https://qcloudimg.tencent-cloud.cn/raw/7d0508a70907b37be34ee78bae12c118.png)
2. 进入升级功能模块界面，单击**立即绑定**，选择未绑定的腾讯特效套餐包，单击**确定**即可升级创建同包名的正式应用，同时解锁腾讯特效模块的正式版 License，无需签发审核。若无可绑定的腾讯特效套餐包，可单击 [资源包购买页](https://buy.cloud.tencent.com/vcube?type=magic) 前往腾讯视立方资源包购买页购买。
<img src="https://qcloudimg.tencent-cloud.cn/raw/20688364d5736456e24b29840c67140f.png" style="zoom:67%;" />
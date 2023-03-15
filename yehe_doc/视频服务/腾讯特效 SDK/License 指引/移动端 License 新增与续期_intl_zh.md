腾讯特效 License 提供美颜特效相关能力，购买腾讯特效SDK套餐或原子能力获得套餐1年使用权限，解锁对应腾讯特效对应功能。计费购买详情请参见 [价格总览](https://www.tencentcloud.com/document/product/1143/45371)。

购买后可在 [腾讯特效控制台](https://console.tencentcloud.com/xmagic) 对腾讯特效 License 进行新增和续期等操作。
本文将对腾讯特效移动端 License 测试版和正式版的新增和续期等操作进行说明指引。

[](id:test)
## 测试版 License

### 申请测试版 License[](id:create_test)

您可以免费申请腾讯特效模块的测试版 License（免费测试有效期为14天，可续期1次，共28天）体验测试。
测试版 License 您可根据自己的需求选择相应的能力进行申请。您可对美颜特效套餐以及原子能力的测试申请；其中套餐仅支持签发最高级版本 S1 - 04 的授权，您可以用此版本测试腾讯特效 SDK套餐全功能，最高级版本 S1 - 04 功能说明请参见 [功能说明](https://www.tencentcloud.com/document/product/1143/45376) 。套餐 S1-04 中包含了 X1-01 人像分割能力，其余能力不包含。

>! **腾讯特效功能模块在申请之后，需要审核通过才能签发授权**，测试版授权到期时间以审核通过时刻为准；若试用期结束后申请测试续期，则续期到期时间以申请测试续期时刻为准。
>- 当提交腾讯特效功能模块测试版审核信息后，进入**审核中状态**，审核时间通常 1-2 个工作日。提交审核信息时间为 `2022-05-24 12:47:33，审核通过时间为 `2022-05-24 15:23:46，则开始时间为 `2022-05-24 15:23:46，14天后到期时间为 `2022-06-09 00:00:00`。
>- 免费续期一次时，若在试用期14天内申请续期，则到期时间为 `2022-06-23 00:00:00；若在试用期14天结束后申请续期，申请续期的时间为 `2022-08-06 22:26:20，则续期的到期时间为 `2022-08-22 00:00:00`。

申请测试模块。您可以选择**新建测试 License 并申请测试功能模块**或在**已创建的测试应用中申请测试新功能模块**两种方式创建测试 License。
<dx-tabs>
::: 方式一：新建测试 License 并申请测试功能模块

1. 登录 [**腾讯特效SDK控制台 > 移动端 License**](https://console.tencentcloud.com/xmagic)，单击**新建测试 License**。
![](https://qcloudimg.tencent-cloud.cn/raw/54ac63cd985f1170b2d74eaac4d0cd1d.png)
2. 根据实际需求填写 `App Name`、`Package Name` 和 `Bundle ID`，选择所需测试的能力 **高级套餐 S1 - 04**、**原子能力X1-01**、**原子能力X1-02**，勾选后准确填写 **公司名称、所属行业类型**，上传**公司营业执照**，单击**确定**提交审核申请，等待人工审核流程。

![](https://qcloudimg.tencent-cloud.cn/raw/e3d3bb59025c79ac4d46f45c67d1cc27.png)
3. 测试版 License 成功创建后，页面会显示生成的 License 信息。此时 Key 和 LicenseURL 两个参数暂未生效，需提交的审核通过后方才生效使用。**在 SDK 初始化配置时需要传入 Key 和 License URL 两个参数，请妥善保存以下信息。**
![](https://qcloudimg.tencent-cloud.cn/raw/6b8d5e0cca6b37e136040a50a17d5099.png)

<dx-alert infotype="explain"> 
1. 测试版 License 有效期内可单击右侧的**编辑**，进入修改 Bundle ID 和 Package Name 信息，单击**确定**即可保存，但会导致此测试 License 下生效中的测试版腾讯特效功能模块**重新进入审核流程**，待审核通过后方可继续使用。
<img src="https://qcloudimg.tencent-cloud.cn/raw/b2a4f9588cc7f0ba5131e631ace94d10.png" style="zoom: 67%;" />
2. 若无 Package Name 或 Bundle Id，可填写“-”。
</dx-alert>

:::
::: 方法二：已创建的测试应用中申请测试新功能模块
若您想在已创建的腾讯特效测试应用中申请新的功能测试模块，步骤如下：
1. 选择您想测试的应用，单击**测试新功能模块**。
![](https://qcloudimg.tencent-cloud.cn/raw/31d21e8d61ed556276a44706a244d804.png)
2. 勾选功能模块 **高级套餐 S1 - 04**/**原子能力X1-01**/**原子能力X1-02**，勾选后准确填写 **公司名称、所属行业类型**，上传**公司营业执照**，单击**确定**提交审核申请，等待人工审核流程。 
<img src="https://qcloudimg.tencent-cloud.cn/raw/99f950a4bb1396e31d69f2c28cdab64f.png" style="zoom:50%;" />
:::
</dx-tabs>

3. 提交审核申请后模块进入**公司资质审核中**，审核时间通常 1-2 个工作日。可单击**查看审核信息**查看提交的审核信息。
<img src="https://qcloudimg.tencent-cloud.cn/raw/a349ab1958dc407c362fad72485dab5d.png" style="zoom:67%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/34446b73133115d11e18b54393361b98.png" style="zoom:67%;" />
4. 审核通过后，腾讯特效功能模块状态为**正常**，腾讯特效测试版 License 申请成功，您可开始使用腾讯特效功能模块。
![](https://qcloudimg.tencent-cloud.cn/raw/516e3b714bd158a452022c4c563e0756.png)
>? **若审核失败**未通过，单击**审核结果**查看审核结果和审核备注，您可根据审核备注知悉审核失败原因，单击**重新发起审核**。更改审核信息并提交，等待人工审核流程。
![](https://qcloudimg.tencent-cloud.cn/raw/d787f5e69875a0de1294a8dd0ab519f3.png)

[](id:renewal_test)
### 续期测试版 License
测试版 License 初次申请默认有效期默认为14天，期满后您可续期**1次**。单击功能模块**腾讯特效**右侧的**续期**，单击**确定续期**即可续期该功能模块14天。
![](https://qcloudimg.tencent-cloud.cn/raw/688ba0f794f4ec63857583a436d78e7a.png)

>? 测试版 License 有效期共28天，**只能续期一次**。若您需继续使用，请购买 [正式版 License](#create_formal)。

[](id:upgrade_test)
### 升级测试版 License
若您需要将腾讯特效模块的测试版 License 升级成为正式版 License，增加使用的有效期，请先 [选择并购买腾讯特效正式版套餐包](https://buy.cloud.tencent.com/vcube?type=magic)，然后执行如下操作：
1. 单击测试版 License 腾讯特效模块中的**升级**。
![](https://qcloudimg.tencent-cloud.cn/raw/d1915913278cbf6f3c188141cdcdea5f.png)
2. 进入升级功能模块界面，单击**立即绑定**，选择未绑定的腾讯特效套餐包，单击**确定**即可升级创建同包名的正式应用，同时解锁腾讯特效模块的正式版 License，无需签发审核。若无可绑定的腾讯特效套餐包，可单击 [资源包购买页](https://buy.cloud.tencent.com/vcube?type=magic) 前往腾讯视立方资源包购买页购买。
<img src="https://qcloudimg.tencent-cloud.cn/raw/9466fa0917c9220d849603ab6a29b190.png" style="zoom:50%;" />

[](id:formal)
## 正式版 License
[](id:create_formal)
### 购买正式版 License
您可根据具体需求场景，在 [腾讯特效 SDK 购买页](https://buy.intl.cloud.tencent.com/vcube) 选择并购买 SDK 特效能力，获得相应的正式版 License 使用授权（有效期 1 年至到期次日00:00:00为止）。各版本 SDK 的功能差异请参见 [计费概述](https://www.tencentcloud.com/document/product/1143/45376)。

具体步骤如下：
1. 绑定腾讯特效正式版 License。您可以选择**新建正式应用并绑定 License**或在**已创建的应用上解锁腾讯特效正式版模块并绑定 License**两种方式进行正式版 License 绑定。 
<dx-tabs>
::: 方式一：新建正式应用并绑定 License
1. 进入 [**腾讯特效控制台 > 移动端 License**](https://console.cloud.tencent.com/vcube)，单击**新建正式 License**。  
![](https://qcloudimg.tencent-cloud.cn/raw/1840aafe0ac1fc54485f9d4a4b15b98a.png) 
2. 填写正式应用的 `App Name`、`Package Name` 和 `Bundle ID` 信息，勾选功能模块**腾讯特效**，单击**下一步**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/f128fdb87a0cc07762bbb75e86b460e9.png" style="zoom:50%;" />
3. 进入选择资源项并绑定 License 界面，单击**立即绑定** ，选择**未绑定**的腾讯特效套餐包（若没有可绑定的资源包，可前往 [资源包购买页](https://buy.cloud.tencent.com/vcube?type=magic) 购买），并单击**确定**即可创建应用并生成正式版 License。 
<img src="https://qcloudimg.tencent-cloud.cn/raw/db5cf0bb61ea8063d25a11dfafb89e90.png" style="zoom:50%;" />
>? 单击**确定**前需要再次确认 Bundle ID 和 Package Name 与业务使用包名信息一致，如与提交到商店的不一致，请在提交前进行修改，**正式版 License 一旦提交成功将无法再修改 License 信息**。 

:::
::: 方式二：已创建的正式版应用中解锁模块
1. 选择您需要增加**腾讯特效**功能模块的正式应用，单击**解锁新功能模块**。
![](https://qcloudimg.tencent-cloud.cn/raw/7d00d56c1dd4c1658f4fde736276d322.png)
2. 选择**腾讯特效**，单击**下一步**。  
![](<img src="https://qcloudimg.tencent-cloud.cn/raw/d88b7f921e294eafec2bbdbaab65edec.png" style="zoom:50%;" />
3. 进入选择资源项并绑定 License 界面，单击**立即绑定** ，选择**未绑定**的腾讯特效套餐包（若没有可绑定的腾讯特效套餐包，可单击 [资源包购买页](https://buy.intl.cloud.tencent.com/vcube) 前往购买），并单击**确定**即可在应用下生成正式版腾讯特效功能模块。
<img src="https://qcloudimg.tencent-cloud.cn/raw/0df1ab29aec13532934eed6457b8936d.png" style="zoom:50%;" />)
:::
</dx-tabs>
2. 腾讯特效功能模块状态为**正常**，腾讯特效正式版 License 申请成功，您可开始使用腾讯特效功能模块。
![](https://qcloudimg.tencent-cloud.cn/raw/75200f8c745038400c568ca5e4d241af.png)


[](id:upgrade_formal)
### 更新正式版 License 有效期
您可以登录  [**腾讯特效SDK控制台 > 移动端 License 管理**](https://console.tencentcloud.com/xmagic)  页面查看腾讯特效正式版 License 的有效期，若您的腾讯特效正式版 License 已到期，可进行如下操作进行续期：
1. 选择您需要更新有效期的 License，单击腾讯特效模块内的**续期**。
![](https://qcloudimg.tencent-cloud.cn/raw/a4b37fc395ce6ea395541825167ad284.png)
2. 选择与原 License **同类型的套餐包**资源进行绑定续期，选择后将实时显示续期的起始时间和结束时间，单击**确定**完成续期。若没有可绑定的腾讯特效套餐包，可单击 [资源包购买页](https://buy.intl.cloud.tencent.com/vcube) 前往购买。
<img src="https://qcloudimg.tencent-cloud.cn/raw/decbe36048335926e3a964a6ae923fbe.png" style="zoom:50%;" />
>!目前续期套餐包有效期仅支持同类型的套餐包续期，即若已绑定的 License 套餐包类型为 S1 - 04，则续期是只能选择 S1 - 04 的套餐包进行续期。若想更改绑定的套餐包类型，需 [提交工单](https://console.intl.cloud.tencent.com/workorder/category) 或联系商务进行处理。
3. 查看更新后的有效期情况。
>! **腾讯特效正式版 License 不支持信息修改**，若您需要修改 License 信息，购买资源包后请勿用于 License 有效期的更新，请单击**创建应用并绑定 License**重新创建应用新增 License 绑定新的包名信息。

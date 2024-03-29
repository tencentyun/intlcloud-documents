本文档介绍如何接入和使用文本内容安全产品（Text Moderation System, TMS）。

## 账号信息获取

### 获取腾讯云账号

登录 [腾讯云控制台](https://console.cloud.tencent.com/) 后，请参考 [账号注册教程](https://intl.cloud.tencent.com/document/product/378/17985) 进行账号注册和实名认证，如果您已经具备腾讯云账号，可以跳过本步骤。

### 获取腾讯云 API 访问密钥

腾讯云通过 secretid 和 secretkey 对开发者的身份和权限进行校验，您可以参考以下步骤获取腾讯云 API 访问密钥：

1. 进入 [云 API 密钥管理](https://console.cloud.tencent.com/cam/capi) 页面，在左侧导航栏选择**访问管理** > **API 密钥管理**，进入 API 密钥管理页面。
2. 单击**新建密钥**创建密钥，并保存 secretid 和 secretkey 供后续 API 调用传参。如果您已经具有腾讯云密钥，可以跳过本步骤。
   ![img](https://qcloudimg.tencent-cloud.cn/raw/1128fbfe6632d7657bfeeacaed9b601c.png)

## 控制台配置

### 服务开通

首次登录 [内容安全控制台](https://console.cloud.tencent.com/cms)，单击**立即开通**

### 权限配置

如果需要通过子账号调用文本内容审核服务，需要对该子账号进行策略授权，具体步骤如下所示：

1. 登录 [访问管理控制台](https://console.cloud.tencent.com/cam/overview)，在左侧导航栏中，选择**用户** > **用户列表**，进入用户列表页面。

2. 在用户列表页面，找到所需的子账户，单击操作列的授权，弹出关联策略弹窗。

   >?  CAM 授权详情请参见 [CAM 授权指引](https://intl.cloud.tencent.com/document/product/1121/43756)。

   ![img](https://qcloudimg.tencent-cloud.cn/raw/3459988e65e5f5100e4f5e075b54c51b.png)

3. 在关联策略弹窗，选择 QcloudTMSFullAccess 策略，单击**确定**，即可保存设置。
   ![img](https://qcloudimg.tencent-cloud.cn/raw/f60457b2e1e07c2e3965c7e5f395820e.png)

### 自定义策略配置（可选）

>? 本步骤为可选操作。如用户不使用自定义审核策略，则可使用默认策略（在 API 调用时，Biztype 字段留空）进行内容审核。

如果您的业务场景需要定制文本内容的审核策略，可以在策略管理中创建自定义策略，配置过程如下所示：

1. 登录 [内容安全控制台](https://console.cloud.tencent.com/cms/image/lib)，在左侧导航栏中，选择**文本内容安全** > **策略管理**，进入策略管理页面。
2. 在策略管理页面，单击左上角的**创建策略**，进入创建策略页面。
3. 填写相关策略信息，按照最接近业务场景的填写即可，其中 Biztype 字段请保留作为 API 传参的入参；**单击下一步**。
   ![img](https://qcloudimg.tencent-cloud.cn/raw/0f33ebc98c517d170726080396b8129a.png)

参数说明

| 参数名称     | 描述                                                         |
| :----------- | :----------------------------------------------------------- |
| 策略名称     | 策略的文字描述，可使用中文、英文、数字及下划线组合，长度不超过30个字符 |
| Biztype名称  | 策略的具体编号，以便用于接口调用，可使用英文、数字及下划线组合，长度为3-32个字符。注：Biztype 名称必须唯一，不可重复 |
| 关联服务模板 | 暂时不需要填写                                               |
| 行业分类     | 策略涉及的行业场景分类                                       |
| 使用行业模板 | 仅**行业分类**有设置时显示。选择是否使用腾讯云预设的行业模板进行审核 |

4. 在策略中勾选需要识别和打击的内容，**单击下一步**。
   ![img](https://qcloudimg.tencent-cloud.cn/raw/f671bacad92169d45c9bed02b24ce8b7.png)

5. 如果您需要识别特定的文本内容，可以在下拉菜单中关联自定义词库，单击下一步

>? 自定义词库的不同颜色代表不同的屏蔽逻辑，红色代表拦截，黄色代表疑似，绿色代表通过。

![img](https://qcloudimg.tencent-cloud.cn/raw/6a0649111cda862d8dd7671e0fcecf8c.png)

6. 核对相关信息无误后，单击完成，即可创建自定义策略。

>? 在 API 传参时，将对应的 Biztype 传入即可使用相应的自定义策略进行文本内容审核。

![img](https://qcloudimg.tencent-cloud.cn/raw/a2c4e83b38df3565735e85bc57d0e5e8.png)
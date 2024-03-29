本文档介绍如何接入和使用视频内容安全（Video Moderation System，VM）。
## 账号信息获取
### 获取腾讯云账号
登录 [腾讯云控制台](https://console.cloud.tencent.com/) 后，请参考 [账号注册教程](https://intl.cloud.tencent.com/document/product/378/17985) 进行账号注册和实名认证，如果您已经具备腾讯云账号，可以跳过本步骤。

### 获取腾讯云 API 访问密钥
腾讯云通过 secretid 和 secretkey 对开发者的身份和权限进行校验，您可以参考以下步骤获取腾讯云 API 访问密钥：
1. 进入 [云 API 密钥管理](https://console.cloud.tencent.com/cam/capi) 页面，在左侧导航栏选择**访问管理** > **API 密钥管理**，进入 API 密钥管理页面。
2. 单击**新建密钥**创建密钥，并保存 secretid 和 secretkey 供后续 API 调用传参。如果您已经具有腾讯云密钥，可以跳过本步骤。
![](https://qcloudimg.tencent-cloud.cn/raw/83e1ef822beff460d607f7f7338f4f6c.png)

## 控制台配置
### 服务开通
首次登录 [内容安全控制台](https://console.cloud.tencent.com/cms/video/overview)，单击**立即开通**，可免费获得**600分钟**的测试套餐包（折合**36000张图片**与**600分钟音频**），有效期为**一个月**。
### 权限配置
如果需要通过子账号调用视频内容服务，需要对该子账号进行策略授权，具体步骤如下所示：
1. 登录 [访问管理控制台](https://console.cloud.tencent.com/cam/overview)，在左侧导航栏中，选择**用户** > **用户列表**，进入用户列表页面。
2. 在用户列表页面，找到所需的子账户，单击操作列的**授权**，弹出关联策略弹窗。
>? CAM 授权详情请参见 [CAM 授权指引](https://intl.cloud.tencent.com/document/product/1140/44981)。 

![](https://qcloudimg.tencent-cloud.cn/raw/a6241d11d5c891e0ab2ec5053515051c.png)
3. 在关联策略弹窗，选择 `QcloudVMFullAccess` 策略，单击**确定**，即可保存设置。
![](https://qcloudimg.tencent-cloud.cn/raw/4106b3a94143d4effaa399c34ba9235e.png)

### 自定义策略配置（可选）
>? 本步骤为可选操作。如用户不使用自定义识别策略，则可使用默认策略（在 API 调用时，Biztype 字段留空）进行内容识别。

如果您的业务场景需要定制视频内容的识别策略，可以在策略管理中创建自定义策略，配置过程如下所示：
1. 登录 [内容安全控制台](https://console.cloud.tencent.com/cms/video/strategy)，在左侧导航栏中，选择**视频内容安全** > **策略管理**，进入策略管理页面。
2. 在策略管理页面，单击左上角的**创建策略**，进入创建策略页面。
3. 填写相关策略信息，按照最接近业务场景的填写即可，其中 Biztype 字段请保留作为 API 传参的入参；**单击下一步**。
![](https://qcloudimg.tencent-cloud.cn/raw/6908d857071825c254fa80c92bfa8507.png)

参数说明
<table>
<thead>
<tr>
<th>参数名称</th>
<th>描述</th>
</tr>
</thead>
<tbody><tr>
<td>策略名称</td>
<td>策略的文字描述，可使用中文、英文、数字及下划线组合，长度不超过30个字符。</td>
</tr>
<tr>
<td>Biztype 名称</td>
<td>策略的具体编号，以便用于接口调用，可使用英文、数字及下划线组合，长度为3-32个字符。  注：Biztype 名称必须唯一，不可重复。</td>
</tr>
<tr>
<td>关联服务模板</td>
<td>目前仅支持使用 default 模板进行模板配置 。</td>
</tr>
<tr>
<td>行业分类</td>
<td>策略涉及的行业场景分类 。</td>
</tr>
<tr>
<td>使用行业模板</td>
<td>仅<strong>行业分类</strong>有设置时显示。  选择是否使用腾讯云预设的行业模板进行识别  。</td>
</tr>
</tbody></table>

4. 在识别策略配置页面，根据业务需求，选择是否需要识别不同类型的识别内容，单击**下一步**。
5. 您可以选择是否需要配置您设定的自定义词库，可以在下拉菜单中关联自定义词库，**单击下一步**。
>? 自定义词库的不同颜色代表不同的屏蔽逻辑，红色代表拦截，黄色代表疑似，绿色代表通过。

![](https://qcloudimg.tencent-cloud.cn/raw/6eb0132e5d1556ca599339d4786f192b.png)
6. 核对相关信息无误后，单击**完成**，即可创建自定义策略。
>? 在 API 传参时，将对应的 Biztype 传入即可使用相应的自定义策略进行视频内容识别。

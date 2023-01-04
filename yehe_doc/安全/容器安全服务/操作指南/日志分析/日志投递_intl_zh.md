支持将日志投递到 [消息队列 CKafka](https://intl.cloud.tencent.com/document/product/597) 和[ 日志服务 CLS](https://intl.cloud.tencent.com/document/product/614) 平台。

## 投递至消息队列 CKafka
1. 在 [日志分析页面](https://console.cloud.tencent.com/tcss/report/logAnalysis)，单击页面上方的**日志投递** > **KAFKA**。
2. 在 KAFKA 页面，单击**立即配置**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/b11621eaa55daace1c85b71624897576.png" style="zoom:50%;" />
3. 在 CKafka 投递配置页面，需授权接入，并配置消息队列实例、公网域名接入、用户名和密码，单击**确定**。
>!
>- 网络接入方式默认选择**公网域名接入**。
>- 投递方式可选择**投递至当前腾讯云账号**或 [投递至其他腾讯云账号](#gw)。

<img src="https://qcloudimg.tencent-cloud.cn/raw/fc1a83b1f4cc78f6925ce4c783ae9664.png" style="zoom:50%;" />

4. 配置完成，确认每一类日志是否开启投递以及投递的 Topic ID/名称。

## 跨账号公网域名投递日志[](id:gw)
### 步骤1：选择投递方式[](id:stpe1)
1. 在 [日志分析页面](https://console.cloud.tencent.com/tcss/report/logAnalysis)，单击页面上方的**日志投递**，并选择 KAFKA 或 CLS。
2. 在 KAFKA 页面，选择**投递至其他腾讯云账号**，并输入接收账号的 uin。
>!
>- **接收账号在腾讯云 [Ckafka 控制台](https://console.cloud.tencent.com/ckafka/index?rid=1) 配置消息实例时，需选择**公网域名方式，并创建3个可接收容器安全服务审计日志的 topic。
>- 将该消息实例的 ID、公网域名，以及接收3类日志所需的 topic ID 和名称记录备份，牢记用户名和密码信息。跨账号授权完成后需在投递账号填写上述信息。

<img src="https://qcloudimg.tencent-cloud.cn/raw/dbec9984378afd041736559b7ecb93f3.png" style="zoom:50%;" />

### 步骤2：配置日志跨账号投递授权
当选择跨账号投递容器安全服务（TCSS）日志时，需在接收账号上授权，允许投递账号核对接收账号的 Ckafka 消息实例、拉取Topic ID和名称等内容。

#### 容器安全服务产品角色已存在
1. 登录 [访问管理控制台](https://console.cloud.tencent.com/cam/role)，在左侧导航中，单击**角色**。
2. 在角色页面的搜索框中，输入 **TCSS**，如检索到下图中的内容，角色名称为：TCSS_QCSRole，角色载体为：产品服务 - tcss。则说明该账号已绑定过容器安全服务产品角色，在关联策略中增加访问管理（CAM）的策略权限和 Ckafka 策略权限即可。
>! 登录的接收账号 uin 需与 [步骤1](#stpe1) 中输入的uin保持一致。

![](https://qcloudimg.tencent-cloud.cn/raw/f29ea25323cd77fc013a0fa83e4aa05f.png)
3. 单击 **TCSS_QCSRole**，进入角色的权限页面。
4. 在权限页面，分别检索策略名 `QcloudCamSubaccountsAuthorizeRoleFullAccess` 和 `QcloudAccessForTCSSRoleInCkafka`。
 - **策略已存在**
    返回 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)登录投递账号，按界面提示测试跨账号策略授权是否成功，成功后配置 Ckafka 日志投递所需的公网域名、消息队列、topic 等信息。
![](https://qcloudimg.tencent-cloud.cn/raw/af6fb4999ac41cf966e59145e197e0b8.png)
 - **策略不存在**
    1. 单击**关联策略**，经过二次确认后，进入关联策略弹窗。
>! 该角色为您授权的服务角色，擅自更改角色内容（角色关联策略或者角色载体）可能导致您授权的服务无法正确使用该角色。

<img src="https://qcloudimg.tencent-cloud.cn/raw/aab03db87b7ac08b2f5650d8c71fd78b.png" style="zoom:67%;" />
    2. 在关联策略弹窗中，分别检索策略名 `QcloudCamSubaccountsAuthorizeRoleFullAccess` 和 `QcloudAccessForTCSSRoleInCkafka`，勾选策略并单击**确定**，即可在 TCSS_QCSRole 角色详情中查看到该条策略。
![](https://qcloudimg.tencent-cloud.cn/raw/79df9c3c28b7f511523f6171b831c074.png)
        3. 配置完成后，返回 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)登录投递账号，按界面提示测试跨账号策略授权是否成功，成功后配置 Ckafka 日志投递所需的公网域名、消息队列、topic 等信息。


#### 容器安全服务产品角色不存在
1. 在 [角色页面](https://console.cloud.tencent.com/cam/role) 的搜索框中，输入 **TCSS**，如检索不到下图中角色名称为：TCSS_QCSRole、角色载体为：产品服务 - tcss 的内容，则说明该账号未绑定过容器安全服务产品的任何策略角色，需在列表中新建角色。
![](https://qcloudimg.tencent-cloud.cn/raw/a1f737e34bd0a4aee562f7700f024889.png)
2. 在角色页面，单击**新建角色**，选择**腾讯云产品服务**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/cdda9b97471f7f3d6a222443fe7ffdcd.png" style="zoom:67%;" />
3. 在输入角色载体信息中，勾选**容器安全服务 (tcss)**，单击**下一步**。
4. 在配置角色策略中，分别检索并勾选策略名 `QcloudCamSubaccountsAuthorizeRoleFullAccess` 和 `QcloudAccessForTCSSRoleInCkafka`，单击**下一步**。
![](https://qcloudimg.tencent-cloud.cn/raw/9da23a47f14362b43972b5dbf10c3d52.png)
5. 在配置角色标签中，用户可自定义或为空，单击**下一步**。
6. 在审阅中，角色名称务必配置为 `TCSS_QCSRole`，容器安全服务严格按该角色名称拉取配置权限；角色描述可用户自定义或为空。配置完成，单击**完成**，验证身份信息后即可在角色页面查看该角色和关联的策略。
![](https://qcloudimg.tencent-cloud.cn/raw/4d4e66c773606866399f89d40731f1ae.png)
7. 配置完成，  返回 [容器安全服务控制台](https://console.cloud.tencent.com/tcss)登录投递账号，按界面提示测试跨账号策略授权是否成功，成功后配置 Ckafka 日志投递所需的公网域名、消息队列、topic 等信息。

## 投递至日志服务 CLS
使用日志服务 CLS 投递时，需授权接入。授权完成后，确认每一类日志是否开启投递以及投递的日志集和日志主题。
1. 在 [日志分析页面](https://console.cloud.tencent.com/tcss/report/logAnalysis)，单击页面上方的**日志投递** > **CLS**。
2. 在 CLS 页面，选择需要投递的日志类型，单击**立即配置**。
<img src="https://qcloudimg.tencent-cloud.cn/raw/5a3c95f0d449af24dc0046e4b735c75f.png" style="zoom:50%;" />
3. 在投递设置页面，配置相关参数，单击**确定**。
>? 当您的账号授权访问日志服务 CLS 服务和开启日志投递到 CLS后，将为您自动在日志服务 CLS 服务中创建后付费的存储空间，同时也会生成后付费账单。具体计费详情请参见 [购买指南](https://intl.cloud.tencent.com/document/product/614/37509)。

<img src="https://qcloudimg.tencent-cloud.cn/raw/4ac92654ed78dd3cba0d0d7b22fb3f73.png" style="zoom:67%;" />


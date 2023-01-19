## 操作场景
账号风控平台默认为每个租户提供50条免费短信，超出免费额度后，平台将暂停为租户发送短信，控制台测试短信、门户短信 OTP 认证源登录都会受影响。为了确保业务的正常使用，管理员需要通过配置短信模板，为平台业务发送短信提供服务。

## 配置短信模板
1. 登录 [账号风控平台](https://console.cloud.tencent.com/ciam)，在左侧导航栏，单击**个性化设置** > **模板设置** > **短信模板**。

2. 在短信模板页面，单击界面右上角的**编辑**。

3. 在编辑页面，分别设置短信服务配置、短信模板配置的相关参数，单击**确定**。

![img](https://qcloudimg.tencent-cloud.cn/raw/305a27c279875c970f919ae60062b444.png)
>? 不同的短信服务配置的参数不同，平台目前**仅支持腾讯云短信服务**，后续会陆续支持其他短信服务的配置。以下为配置腾讯云短信服务所需要的相关参数。

### 短信服务配置
####  获取 SDK AppID
1. 登录 [腾讯云短信控制台](https://console.cloud.tencent.com/smsv2)，在左侧导航栏，选择**应用管理** > **应用列表**，进入应用列表页面。
2. 在应用列表页面，单击**创建应用**，输入应用名称、简介和标签，单击**创建**，即可完成创建应用。
   ![img](https://qcloudimg.tencent-cloud.cn/raw/9fb501511973763e47f74f82920b48a7.png)
3. 在应用列表页面，选择所需应用，单击![](https://qcloudimg.tencent-cloud.cn/raw/0aa6ed67999bf503415c391177264941.png)获取该应用的 SDK AppID。
   ![img](https://qcloudimg.tencent-cloud.cn/raw/724fe2cc923fd53679e351c270135084.png)

#### 获取 SecretId 和 SecretKey
1. 登录 [访问管理控制台](https://console.cloud.tencent.com/cam/overview)，在左侧导航栏，选择**用户** > **用户列表**，进入用户列表页面。
2. 在用户列表页面，选择所需子账号，单击**用户名称**，进入用户详情页面。
3. 在用户详情页面，单击 **API 密钥**，选择所需密钥，单击![](https://qcloudimg.tencent-cloud.cn/raw/0aa6ed67999bf503415c391177264941.png)获取该子账号的 SecretId；单击**显示**，身份校验成功后，即可获取该子账号的 SecretKey。
   
### 短信模板配置
短信模板设置需要获取发送短信所需的短信签名和短信模板 ID，获取获取方法如下：
#### 获取短信签名
1. 登录[ 短信服务控制台](https://console.cloud.tencent.com/smsv2)，在左侧导航栏，选择**国际短信** > **签名管理**，进入签名管理页面。
2. 在签名管理页面，单击**创建签名**，填写相关参数，单击**确定**。
![img](https://qcloudimg.tencent-cloud.cn/raw/85c2234c81b711647d38e90a51d74982.png)
3. 审核通过后，可以在签名管理页面，查看短信签名。

#### 获取短信模板 ID
1. 登录[ 短信服务控制台](https://console.cloud.tencent.com/smsv2)，在左侧导航栏，选择**国际短信** > **正文模板管理**，进入正文模板管理页面。
2. 在正文模板管理页面，单击**创建正文模板**，填写相关参数，单击**确定**即可。
![img](https://qcloudimg.tencent-cloud.cn/raw/198eb832687a1796828b428eb1af64d5.png)
3. 审核通过后，可以在正文模板管理页面，查看短信模板 ID。
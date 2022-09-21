## 验证码调用时序图

### Web/App客户端

Web/App客户端调用验证码的时序图如下：

- 业务客户端：需接入验证码，在客户端展示验证页面。
- 业务服务端：需调用票据校验 API，对客户端验证结果进行二次校验。 

![](https://qcloudimg.tencent-cloud.cn/raw/6cb8455c3891dc4574fa72144366013d.png)

## 快速接入

### 步骤1：新建验证，获取验证码密钥

1. 登录 [验证码控制台](https://console.cloud.tencent.com/captcha/graphical) ，左侧导航栏选择**图形验证** > **验证管理**，进入验证管理页面。
2. 单击**新建验证**，根据业务场景需求，设置验证名称等参数。
3. 单击**确定**，完成新建验证，即可在验证列表中查看验证码密钥（ CaptchaAppId 及 AppSecretKey）。

>! 创建验证后，仍可进行验证方式、风控等级、外观样式的修改，详情参见[控制台操作指南](https://intl.cloud.tencent.com/document/product/1159/49686)。

### 步骤2：客户端接入验证码，展示验证页面

Web/App客户端代码需动态引入验证码js，在业务需要行为验证时，调用并渲染验证码js进行验证。详情参见  [Web 客户端接入](https://intl.cloud.tencent.com/document/product/1159/49680)、  [App 客户端接入](https://intl.cloud.tencent.com/document/product/1159/49681)。

>! 必须动态加载TCaptcha-global.js。如通过其他手段规避动态加载，会导致验证码无法正常更新，对抗能力无法保证，甚至引起误拦截。

### 步骤3：服务端接入验证码，调用票据校验 API 进行二次校验

服务端需调用票据校验API（DescribeCaptchaResult），对客户端验证结果进行二次校验。 详情参见  [接入票据校验（Web 及 App）](https://intl.cloud.tencent.com/document/product/1159/49682)。

>! 未接入票据校验，会导致黑产轻易伪造验证结果，失去验证码人机对抗效果。

## 更多功能

验证码控制台还支持以下功能：
- **数据统计**：查看请求量、验证通过量、验证拦截量、票据校验量等统计数据。
- **验证配置**： 验证码安全、外观等相关配置调整。

详情参见 [控制台操作指南](https://intl.cloud.tencent.com/document/product/1159/49686)。

## 常见问题

详情参见 [接入相关问题](https://intl.cloud.tencent.com/document/product/1159/49692)。

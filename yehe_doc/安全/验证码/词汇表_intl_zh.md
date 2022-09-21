### CaptchaAppId

验证码应用ID，接入验证码时，需要填写该参数。业务客户端在调用验证码服务时，验证码服务器通过CaptchaAppId可获取到您在控制台上配置的验证类型、风控等级等参数。CaptchaAppId及AppSecretKey可在 [验证码控制台](https://console.cloud.tencent.com/captcha/graphical) 验证列表页进行查看。

### SecretKey

SecretId 和 SecretKey 合称为云 API 密钥，是用户访问腾讯云 API 进行身份验证时需要用到的安全凭证。SecretKey 是用于加密签名字符串和服务器端验证签名字符串的密钥。一个 APPID 可以创建多个云 API 密钥。

### 验证码票据

业务客户端发起验证后，回调函数返回的用户验证票据（Ticket），在业务服务端调用票据校验API时需要该参数。

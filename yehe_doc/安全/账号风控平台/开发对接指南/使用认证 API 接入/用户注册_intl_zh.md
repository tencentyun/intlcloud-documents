## 接口描述
注册新用户。此接口适用于**应用系统自行开发注册功能的场景**，如果您的应用使用了 CIAM 认证门户，请参考 [使用认证门户注册](https://www.tencentcloud.com/document/product/1148/51469)。

调用此接口前，请确认已配置并启用了应用的注册流程。接口入参需要遵循注册流程中配置的业务规则。例如，注册流程配置了电话号码作为认证属性，用户昵称作为必填普通属性，则入参中必须包含电话号码和用户昵称这两个属性；**如果注册流程未配置电话号码作为认证属性，则入参中不能包含电话号码**。

注册信息中包含电话号码或邮箱地址时，需要先调用 [发送 OTP 验证码 ](https://www.tencentcloud.com/document/product/1148/51475) 接口向用户发送验证码。

密码为可选参数，您可以根据具体业务情况决定是否要求用户设置密码。
- 如果用户仅通过短信 OTP、邮箱 OTP 或社交认证方式登录，可以不设置密码。
- 如需支持用户通过账号密码认证登录，则应设置密码。

如果需要设置密码，请确保应用的登录流程中**关联了账号密码认证源**，接口将根据该认证源的密码策略对传入密码进行校验，如果密码不满足策略要求则无法成功完成注册。
>?
>- 此接口不支持设置用户组。注册成功的用户默认归属注册流程中配置的用户组。
>- 此接口不处理自动登录和实名认证逻辑。即注册流程中的自动登录和实名认证相关配置对此接口不生效。

## 支持的应用类型
Web 应用。

## 请求方法
```
POST
```

## 请求路径
```
/signup
```

## 请求 Content-Type
```
application/json
```

## 请求示例
- 使用用户名注册，并设置密码。
```
POST /signup HTTP/1.1
Content-Type: application/json
Authorization: Basic VEVOQU5UX0NMSUVOVF9JRDpURU5BTlRfQ0xJRU5UX1NFQ1JFVA==
Host: sample.portal.tencentciam.com

{
  "username" : "MOCK_USERNAME",
  "password" : "MOCK_PASSWORD"
}
```
- 使用邮箱和昵称注册，并设置密码。
```
POST /signup HTTP/1.1
Content-Type: application/json
Authorization: Basic VEVOQU5UX0NMSUVOVF9JRDpURU5BTlRfQ0xJRU5UX1NFQ1JFVA==
Host: sample.portal.tencentciam.com

{
  "email" : "MOCK_USERNAME@example.com",
  "email_otp_token" : "MOCK_EMAIL_OTP_TOKEN",
  "email_otp" : "MOCK_EMAIL_OTP",
  "password" : "MOCK_PASSWORD",
  "nickname" : "MOCK_NICKNAME"
}
```
- 使用电话号码注册，不设置密码。
```
POST /signup HTTP/1.1
Content-Type: application/json
Authorization: Basic VEVOQU5UX0NMSUVOVF9JRDpURU5BTlRfQ0xJRU5UX1NFQ1JFVA==
Host: sample.portal.tencentciam.com

{
  "phone_number" : "13612345678",
  "phone_number_otp_token" : "MOCK_PHONE_NUMBER_OTP_TOKEN",
  "phone_number_otp" : "MOCK_PHONE_NUMBER_OTP"
}
```

## 请求头

| 名称          | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| Authorization | HTTP Basic 认证请求头，格式为 `Basic <credentials>`，其中 `Basic` 为固定字符串，`<credentials>`  的计算方式为 `base64(url_encode(client_id) + ":" + url_encode(client_secret))`，`Basic` 和 `<credentials>` 之间用一个空格隔开。 |

## 请求体 JSON 参数
| JSON 路径              | 数据类型 | 描述                                                         |
| :--------------------- | :------- | :----------------------------------------------------------- |
| username               | String   | 用户名，可以包含英文字母、数字和下划线，必须以字母开始，最长32个字符。 |
| password               | String   | 用户密码。如果设置，则必须符合应用关联的账号密码认证源的密码策略。 |
| phone_number           | String   | 用户的手机号，限国内三大运营商11位手机号。传递此参数时，须同时传递 `phone_number_otp_token` 和 `phone_number_otp` 两个参数。 |
| phone_number_otp_token | String   | 发送短信验证码成功后服务端返回的 `otp_token`。               |
| phone_number_otp       | String   | 用户手机收到的 OTP 验证码。                                  |
| email                  | String   | 用户的邮箱地址。传递此参数时，须同时传递 `email_otp_token` 和 `email_otp` 两个参数。 |
| email_otp_token        | String   | 发送邮箱验证码成功后服务端返回的 `otp_token`。               |
| email_otp              | String   | 用户邮箱收到的 OTP 验证码。                                  |
| name                   | String   | 用户姓名。                                                   |
| nickname               | String   | 用户昵称。                                                   |
| zoneinfo               | String   | 用户时区，如 `Asia/Shanghai` 或 `Europe/Paris`。             |
| locale                 | String   | 用户 locale 信息，如 `zh-CN` 或 `en-US`。                    |

>? 其他参数的取值为用户属性标识。属性标识可以在 [属性自定义页面](https://console.cloud.tencent.com/ciam/custom-attributes) 的属性详情界面查看。

## 注册成功响应示例
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "sub" : "MOCK_USER_ID"
}
```

## 响应参数
| 字段 | 数据类型 | 描述           |
| :--- | :------- | :------------- |
| sub  | String   | 用户唯一标识。 |

## 注册失败响应示例
- 应用注册流程未启用。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "misconfigured",
  "error_description" : "Sign up flow of the application is not enabled."
}
```
- 入参缺少注册流程配置的认证属性或必填普通属性。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_request",
  "error_description" : "Missing required sign-up attribute(s)."
}
```
- 入参包含注册流程未配置的认证属性或普通属性。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_request",
  "error_description" : "Unconfigured sign-up attribute(s) found."
}
```
- 入参包含未知属性。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_request",
  "error_description" : "Unknown attribute(s) found."
}
```
- 用户名格式不合法。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_username"
}
```
- 用户名已存在。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "duplicate_username"
}
```
- 电话号码格式不合法。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "malformed_phone_number"
}
```
- 电话号码已存在。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "duplicate_phone_number"
}
```
- `phone_number_otp_token` 错误或已过期，或注册时使用的参数与发送验证码时不一致（例如：手机号不同）。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "bad_phone_number_otp_token"
}
```
- `phone_number_otp` 错误或已过期。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "bad_phone_number_otp"
}
```
- 邮箱格式不合法。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "malformed_email"
}
```
- 邮箱已存在。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "duplicate_email"
}
```
- `email_otp_token` 错误或已过期，或注册时使用的参数与发送验证码时不一致（例如：邮箱不同）。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "bad_email_otp_token"
}
```
- `email_otp` 错误或已过期。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "bad_email_otp"
}
```
- 入参中传入了密码，但应用登录流程中未关联账号密码认证源。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "misconfigured",
  "error_description" : "No password auth source is associated with the application."
}
```
- 密码不满足策略要求。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_password"
}
```
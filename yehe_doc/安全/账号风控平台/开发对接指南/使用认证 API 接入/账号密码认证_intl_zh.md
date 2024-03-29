## 接口描述
校验用户的用户名和密码，获取 Access Token 和 ID Token，完成登录。此接口对应 OAuth 2.0 协议的 Resource Owner Password Credentials 模式。
>? 由于用户密码将在用户终端与应用之间传递，请务必使用高度可信的应用调用此接口，并妥善处理密码的传输（例如确保使用了 HTTPS 协议）。在条件允许的情况下，建议优先使用 [认证门户登录](https://www.tencentcloud.com/document/product/1148/51469)。

## 支持的应用类型
Web 应用、单页应用、移动 App。

## 请求方法
```
POST
```
## 请求路径
```
/oauth2/token
```

## 请求 Content-Type
```
application/x-www-form-urlencoded
```

## 请求示例
```
POST /oauth2/token HTTP/1.1
Host: sample.portal.tencentciam.com
Content-Type: application/x-www-form-urlencoded
grant_type=password&client_id=TENANT_CLIENT_ID&client_secret=TENANT_CLIENT_SECRET&auth_source_id=MOCK_USERNAME_PASSWORD_AUTH_SOURCE_ID&username=MOCK_USERNAME&password=MOCK_PASSWORD&scope=openid
```


## 请求参数
| 参数           | 可选  | 描述                                                         |
| :------------- | :---- | :----------------------------------------------------------- |
| grant_type     | false | 填固定值 `password`。                                        |
| client_id      | false | 应用的 `client_id`。可参考 **[应用管理页面](https://console.cloud.tencent.com/ciam/app-management)** > **选定指定应用** > 单击**应用配置** > 对应的“Client Id”。 |
| client_secret  | true  | 应用的 `client_secret`。可参考 **[应用管理页面](https://console.cloud.tencent.com/ciam/app-management)** > **选定指定应用** > 单击**应用配置** > 对应的“client_secret”。<li>Web 应用须传递此参数。</li><li>单页应用和移动 App 不传递此参数。</li> |
| auth_source_id | false | 账号密码认证源 ID。可在控制台的 [通用认证源页面](https://console.cloud.tencent.com/ciam/general-auth-source) 查看。 |
| username       | false | 用户名。需要使用账号密码认证源配置的认证源属性，如用户名称、电话号码、邮箱地址。 |
| password       | false | 用户密码。                                                   |
| scope          | true  | 可省略。如传递，则填固定值 `openid`。                        |


## 正常响应示例
#### 认证成功
```
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
  "access_token" : "eyJraWQiOiI1MzQyOGU3ZS1kOTJiLTQ3OTAtOGIwMC0wMmEyZjc4NjUxNzMiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJNT0NLX1VTRVJfSUQiLCJhdWQiOiJURU5BTlRfQ0xJRU5UX0lEIiwibmJmIjoxNjQwNTg4ODI2LCJzY29wZSI6WyJvcGVuaWQiXSwiaXNzIjoiaHR0cHM6XC9cL3NhbXBsZS5wb3J0YWwudGVuY2VudGNpYW0uY29tIiwiZXhwIjoxNjQwNTg5MTI2LCJpYXQiOjE2NDA1ODg4MjYsImp0aSI6IjU0ODZhNWRhLTE0YTYtNDNkZC04MWNkLTEwNmRiMDVhMjJmZiJ9.cd2hoQEVZLGcRaqhDLs-W8m9IN2pDT4XzluxYz4ulNwHTfBTu_1NamlH0kmd0KDhzBMRAl6YXHVDVOXZEV47C1uoYDATnwQetUsg8eJObzlPEVZ81ovU-eRm7I0lQ_MVI9MC7jMcdOKvEDJCOJtnwtorkQpqEPYovrxctNvvClqLBsDVbUebC2-iUGwz4vWE-DL17M39rqtmwXv6C21ovv6Pe9BSUUAj_CzHSV-ZSF7fjyYjnlTEOLjilFNsFD9Ow1czNFqnwxkc7dwugOGJ7qM30zuTgSme76K3tLbol8fKO-CUKglZO9mWIXUWizhePTzd3CKGE4C7gUHR40EjNw",
  "refresh_token" : "7uqTlthTQrzIZx8joT20chQbakZp81_iv39GTyCpsEyYpWoquNhuB3s6qEQHGeu2RBpaZcavFf9UOdgtUaCjB42D478MISnj6qBY52q3Pd5eNBBcXZ68oqMkFVidvgha",
  "scope" : "openid",
  "id_token" : "eyJraWQiOiI1MzQyOGU3ZS1kOTJiLTQ3OTAtOGIwMC0wMmEyZjc4NjUxNzMiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJNT0NLX1VTRVJfSUQiLCJhdWQiOiJURU5BTlRfQ0xJRU5UX0lEIiwiYXpwIjoiVEVOQU5UX0NMSUVOVF9JRCIsImlzcyI6Imh0dHBzOlwvXC9zYW1wbGUucG9ydGFsLnRlbmNlbnRjaWFtLmNvbSIsImV4cCI6MTY0MDU5MDYyNiwiaWF0IjoxNjQwNTg4ODI2LCJqdGkiOiI0Mzg0OTUwYS0zOTFlLTQ3MDgtYjFjYS05ZjVkNzQzN2Q3ZDIifQ.kaquINkB64dRAaXPG8KLBCpZ6hwNxtA5ruXpwYgEzFHppXQMqPRQQ-Iwn0659lpy8B2CqjRIar_A1xS518Uua3ItkUtoJQXcIxLDSGRatk6mZ6q7XgOHvALsLhQlYQjn36kXdnOJipPVB124y-o20UHwUC27nUH0e9GuYxwX3p56684NB4xJXUfEL2yl9Zt8rMEpD1I1hI5exg75ZP7MCSjzoNgr7fmpGuDNWWhRALh6sY4Dv5BSgE9B0No0xwFOLnAV4NMsvimJg5rBlJXepOhW4JfwZ3TnzXtDUk3oeajhRxPtjbkxt5NrSYMxUwBggkcoi4eOfVpo8crmQNrSVQ",
  "token_type" : "Bearer",
  "expires_in" : 299
}
```

#### 响应参数
| 参数          | 数据类型 | 描述                                      |
| :------------ | :------- | :---------------------------------------- |
| access_token  | String   | OAuth 2.0 Access Token (JWT)。            |
| token_type    | String   | Token 类型，目前返回的是固定值 `Bearer`。 |
| expires_in    | Number   | Access Token 有效期，单位秒。             |
| scope         | String   | Access Token scope。                      |
| refresh_token | String   | OAuth 2.0 Refresh Token。                 |
| id_token      | String   | OIDC ID Token (JWT)。                     |


## 异常响应示例
- 用户名密码错误。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant",
  "error_description" : "Wrong username or password"
}
```

- 用户状态异常（如被锁定或冻结）。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant",
  "error_description" : "Abnormal user status"
}
```

- 使用了认证源不支持的属性作为用户名（例如：username 传入了邮箱地址，但账号密码认证源未配置邮箱地址为认证源属性）。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant",
  "error_description" : "Unsupported username identifier"
}
```
- 认证源不是应用的首选认证源或关联认证源。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_auth_source",
  "error_description" : "Auth source and application not associated"
}
```
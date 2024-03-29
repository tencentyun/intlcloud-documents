## 接口描述
使用 OAuth 客户端凭证模式 (client_credentials) 获取 Access Token 。

## 支持的应用类型
Web 应用、M2M 应用。

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

grant_type=client_credentials&client_id=TENANT_CLIENT_ID&client_secret=TENANT_CLIENT_SECRET&scope=identity_proofing
```


## 请求参数
| 参数          | 可选  | 描述                                                         |
| :------------ | :---- | :----------------------------------------------------------- |
| grant_type    | false | 填固定值 `client_credentials`。                              |
| client_id     | false | 应用的 `client_id `。可参考 **[应用管理页面](https://console.cloud.tencent.com/ciam/app-management)** > **选定指定应用** > 单击**应用配置** > 对应的“Client Id”。 |
| client_secret | false | 应用的 `client_secret` 。可参考 **[应用管理页面](https://console.cloud.tencent.com/ciam/app-management)** > **选定指定应用** > 单击**应用配置** > 对应的“client_secret”。 |
| scope         | true  | 申请授权的 `scope`，多个 `scope` 之间使用空格分隔。          |




## 正常响应示例
```
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
  "access_token" : "eyJraWQiOiJmOTY5NGQ5My1kNTQxLTQ5ODUtODhkYy00MjIyOTg3MzAwOGUiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJURU5BTlRfQ0xJRU5UX0lEIiwiYXVkIjoiVEVOQU5UX0NMSUVOVF9JRCIsIm5iZiI6MTY0MDU4ODgyOCwic2NvcGUiOlsiaWRlbnRpdHlfcHJvb2ZpbmciXSwiaXNzIjoiaHR0cHM6XC9cL3NhbXBsZS5wb3J0YWwudGVuY2VudGNpYW0uY29tIiwiZXhwIjoxNjQwNTg5MTI4LCJpYXQiOjE2NDA1ODg4MjgsImp0aSI6Ijk5MzliYzNmLTVlZGYtNDZjMy04ZjVjLTJiMWRjMWFjZmE5MCJ9.D8khbU3BkWTHD6sRTY9M_bbRq7AF4MGina2S1ycFA2HOUo-k_P_f81V4fP1DLO7n-1_5em_Dmxo768wsFcvUIYWRlSLh91kXPTyBV5mHt6IZRnT3eMpqTiMKC_ubzUc_7DSpE8-99-CpfrQ19hcpMwkoLYh1dwYjUJB6xyZPzqlezrHy4unUHLTpyjGeecgNNLUScY9W0diGxVnbsMuTW7T00OsltNoJj11qtOllbh5kd1B4umvA3UJpGucVMZQ2YTvltHyDBefWabP4ektzktAwDTALGIu1EsQfb5j9Rru3R0L0nAvjT8HiIqthLvvMdkjXAW983zj0yCPe3GqF3g",
  "scope" : "identity_proofing",
  "token_type" : "Bearer",
  "expires_in" : 299
}
```


## 响应参数
| 参数         | 数据类型 | 描述                                      |
| :----------- | :------- | :---------------------------------------- |
| access_token | String   | Access Token (JWT)。                      |
| token_type   | String   | Token 类型，目前返回的是固定值 `Bearer`。 |
| expires_in   | Number   | Access Token 有效期，单位秒。             |
| scope        | String   | Access Token 的 Scope。                   |

>？客户端凭证模式的响应中不包含 Refresh Token。当 Access Token 过期时，应用再次调用此接口获取新的 Access Token。


## 异常响应示例
- 应用不存在、未开启或应用密钥校验失败。
```
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_client"
}
```

- 应用无权限使用 `client_credentials` 模式获取 Token。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "unauthorized_client"
}
```

- scope 参数有误或超出应用权限。
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_scope"
}
```
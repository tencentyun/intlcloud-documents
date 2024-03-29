## 接口描述
获取已登录用户的用户信息。调用此接口时，需携带登录成功时得到的具备 `openid scope` 的 Access Token。


## 支持的应用类型
Web 应用、单页应用、移动 App、M2M 应用。

## 请求方法
```
GET
```
## 请求路径
```
/userinfo
```

## 请求示例
```
GET /userinfo HTTP/1.1
Authorization: Bearer ACCESS_TOKEN_WITH_OPENID_SCOPE
Host: sample.portal.tencentciam.com
```

## 请求头
| 名称          | 描述                                                         |
| :------------ | :----------------------------------------------------------- |
| Authorization | OAuth 2.0 Bearer Token，格式为 `Bearer <Token>`，其中 `Bearer` 为固定字符串，`<Token>` 为用户登录成功时得到的具备 `openid scope` 的 Access Token，`Bearer` 和 `<Token>` 之间用一个空格隔开。 |


## 正常响应示例
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "sub" : "MOCK_USER_ID",
  "email" : "MOCK_USERNAME@example.com",
  "name" : "MOCK_NAME",
  "nickname" : "MOCK_NICKNAME",
  "zoneinfo" : "Asia/Shanghai",
  "locale" : "zh-CN"
}
```


## 响应参数

| 参数 | 数据类型 | 描述                       |
| :--- | :------- | :------------------------- |
| sub  | String   | 用户标识，在用户池内唯一。 |


>? 除 `sub` 字段一定返回外，其余返回哪些字段由应用参数配置中的 `Claims` 决定。


## 异常响应示例
- 未携带 Access Token。
```
HTTP/1.1 400 Bad Request
WWW-Authenticate: Bearer error="invalid_request", error_description="Bearer token not found in the request", error_uri="https://tools.ietf.org/html/rfc6750#section-3.1"
```
- Access Token 无效（例如 Token 格式有误、已过期或已注销）。
```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer error="invalid_token", error_description="Error decoding JWT", error_uri="https://tools.ietf.org/html/rfc6750#section-3.1"
```
- Access Token 不具备 `openid scope`。
```
HTTP/1.1 403 Forbidden
WWW-Authenticate: Bearer error="insufficient_scope", error_description="The request requires higher privileges than provided by the access token.", error_uri="https://tools.ietf.org/html/rfc6750#section-3.1"
```
- 找不到 Access Token 对应的用户。
```
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
  "error" : "user_not_found"
}
```
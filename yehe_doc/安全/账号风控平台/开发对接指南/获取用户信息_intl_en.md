## API Description
This API is used to get the user information of a logged-in user. When calling this API, you need to carry the Access Token with `openid scope` returned when the login is successful.


## Supported Applications
Web applications, single-page applications (SPA), mobile applications, and machine-to-machine (M2M) applications.

## Request Method
```
GET
```
## Request Path
```
/userinfo
```

## Sample Requests
```
GET /userinfo HTTP/1.1
Authorization: Bearer ACCESS_TOKEN_WITH_OPENID_SCOPE
Host: sample.portal.tencentciam.com
```

## Request Headers
| Parameter | Description |
| :------------ | :----------------------------------------------------------- |
| Authorization | OAuth 2.0 Bearer Token. The format is `Bearer <Token>`, where `Bearer` is a fixed string and `<Token>` is the Access Token with `openid scope` returned when the login is successful. `Bearer` and `<Token>` are separated by a space. |


## Sample Success Responses
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


## Response Parameters

| Parameter | Data Type | Description |
| :--- | :------- | :------------------------- |
| sub | String | Unique identifier of the user in the user pool. |


>? Only the `sub` parameter must be returned, and other parameters returned are determined by `Claims` in the application parameter configuration.


## Sample Error Responses
- No Access Token.
```
HTTP/1.1 400 Bad Request
WWW-Authenticate: Bearer error="invalid_request", error_description="Bearer token not found in the request", error_uri="https://tools.ietf.org/html/rfc6750#section-3.1"
```
- The Access Token is invalid. For example, the Token format is invalid. The Token has expired or has been revoked.
```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer error="invalid_token", error_description="Error decoding JWT", error_uri="https://tools.ietf.org/html/rfc6750#section-3.1"
```
- The Access Token does contain `openid scope`.
```
HTTP/1.1 403 Forbidden
WWW-Authenticate: Bearer error="insufficient_scope", error_description="The request requires higher privileges than provided by the access token.", error_uri="https://tools.ietf.org/html/rfc6750#section-3.1"
```
- No user found for the Access Token.
```
HTTP/1.1 404 Not Found
Content-Type: application/json;charset=UTF-8

{
  "error" : "user_not_found"
}
```

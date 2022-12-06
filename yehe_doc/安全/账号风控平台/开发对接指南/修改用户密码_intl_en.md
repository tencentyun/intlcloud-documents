## API Description
This API is used to modify the password of a logged-in user. When calling this API, you need to carry the Access Token with `openid scope` returned when the login is successful. The new password must comply with the policies of the account and password authentication source associated with the application. It cannot be the same as the previous N passwords specified in the policy.



## Supported Applications
Web applications, single-page applications (SPA), mobile applications, and machine-to-machine (M2M) applications.

## Request Method
```
POST
```
## Request Path
```
/change_user_password
```

## Request Content-Type
```
application/json
```

## Sample Requests
```
POST /change_user_password HTTP/1.1
Content-Type: application/json
Authorization: Bearer ACCESS_TOKEN_WITH_OPENID_SCOPE
Host: sample.portal.tencentciam.com

{
  "old_password" : "MOCK_PASSWORD",
  "new_password" : "MOCK_NEW_PASSWORD"
}
```

## Request Headers
| Parameter | Description |
| :------------ | :----------------------------------------------------------- |
| Authorization | OAuth 2.0 Bearer Token. The format is `Bearer <Token>>`, where `Bearer` is a fixed string and `<Token>` is the Access Token with `openid scope` returned when the login is successful. `Bearer` and `<Token>` are separated by a space. |

## Request Parameters in JSON Format
| JSON Path | Data Type | Description |
| :----------- | :------- | :------- |
| old_password | String | Old password. |
| new_password | String | New password. |




## Sample Success Responses
```
HTTP/1.1 200 OK
```

## Sample Error Responses
- The old password is incorrect.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "wrong_old_password"
}
```
- The new password is the same as the old one.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "duplicate_password"
}
```
- The new password is the same as a previous password.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "recurrent_password"
}
```
- The new password does not comply with the password policy.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_new_password"
}
```
- User not found.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "user_not_found"
}
```
- The user account is frozen.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "abnormal_user_status",
  "error_description" : "User is frozen."
}
```
- The user account is locked.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "abnormal_user_status",
  "error_description" : "User is locked."
}
```
- The `bearer_token` parameter is missing.
```
HTTP/1.1 400 Bad Request
WWW-Authenticate: Bearer error="invalid_request", error_description="Bearer token not found in the request", error_uri="https://tools.ietf.org/html/rfc6750#section-3.1"
```
- The `bearer_token` parameter is incorrect.
```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Bearer error="invalid_token", error_description="Error decoding JWT", error_uri="https://tools.ietf.org/html/rfc6750#section-3.1"
```
- The `bearer_token` parameter is invalid.
```
HTTP/1.1 403 Forbidden
WWW-Authenticate: Bearer error="insufficient_scope", error_description="The request requires higher priv
```
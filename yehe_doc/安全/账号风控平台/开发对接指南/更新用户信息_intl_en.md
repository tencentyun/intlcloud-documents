## API Description
This API is used to update the personal information of a logged-in user. When calling this API, you need to carry the Access Token with `openid scope` returned when the login is successful. To change the mobile number or email address, call the [API for sending one-time password (OTP) verification code](https://www.tencentcloud.com/document/product/1148/51475) to send a verification code to the user.



## Supported Applications
Web applications, single-page applications (SPA), mobile applications, and machine-to-machine (M2M) applications.

## Request Method
```
PATCH
```
## Request Path

```
/userinfo
```
## Request Content-Type
```
application/json
```

## Sample Requests
```
PATCH /userinfo HTTP/1.1
Content-Type: application/json
Authorization: Bearer ACCESS_TOKEN_WITH_OPENID_SCOPE
Host: sample.portal.tencentciam.com

{
  "nickname" : "MOCK_NICKNAME"
}
```

## Request Headers
| Parameter | Description |
| :------------ | :----------------------------------------------------------- |
| Authorization | OAuth 2.0 Bearer Token. The format is `Bearer <Token>>`, where `Bearer` is a fixed string and `<Token>` is the Access Token with `openid scope` returned when the login is successful. `Bearer` and `<Token>` are separated by a space. |

## Request Parameters in JSON Format
| JSON Path | Data Type | Description |
| :--------------------- | :------- | :----------------------------------------------------------- |
| phone_number | String | The user's mobile number, which should be an 11-digit mobile number of the three major carriers in Chinese mainland. When this parameter is specified, both `phone_number_otp_token` and `phone_number_otp` are required. |
| hone_number_otp_token | String | The `otp_token` returned by the server after the SMS verification code is sent.               |
| phone_number_otp | String | The OTP verification code received by the user's mobile phone.                                  |
| email | String | The user's email address. When this parameter is specified, both `email_otp_token` and `email_otp` are required. |
| email_otp_token        | String   | The `otp_token` returned by the server after the email verification code is sent.               |
| email_otp | String | The OTP verification code received by the user's email.                                  |
| Name             | String           | Username                                                         |
| nickname               | String   | The user's alias.                                                   |
| zoneinfo               | String   | The user’s time zone, such as `Asia/Shanghai` or `Europe/Paris`.             |
| locale | String | The user `locale` information, such as `zh-CN` or `en-US`.                    |

>? The values of other parameters are user attribute identifiers. The attribute identifiers can be viewed on the [Custom Attributes page](https://console.cloud.tencent.com/ciam/custom-attributes).


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
>? Only the `sub` parameter must be returned, and other parameters returned are determined by `Claims` in the application parameter configuration.


## Sample Error Responses
- The input parameters contain unknown attributes.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_request",
  "error_description" : "Unknown attribute(s) found."
}
```
- The input parameters contain attributes that cannot be modified.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_request",
  "error_description" : "Unsupported user attribute(s) found."
}
```
- The mobile number format is invalid.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "malformed_phone_number"
}
```
- The mobile number already exists.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "duplicate_phone_number"
}
```
- The `phone_number_otp_token` parameter is incorrect or has expired, or the parameter used for sign-up is not the same as the one for sending the verification code. For example, the mobile numbers are different.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "bad_phone_number_otp_token"
}
```
- The `phone_number_otp` parameter is incorrect or has expired.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "bad_phone_number_otp"
}
```
- The email address format is invalid.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "malformed_email"
}
```
- The email address already exists.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "duplicate_email"
}
```
- The `email_otp_token` parameter is incorrect or has expired, or the parameter value used for sign-up is not the same as the one used for sending the verification code. For example, the email addresses are different.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "bad_email_otp_token"
}
```
- The `email_otp` parameter is incorrect or has expired.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "bad_email_otp"
}
```
- The input parameter value is invalid. For example, the value does not conform to the regular expression of user attributes.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "illegal_parameter_value"
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
WWW-Authenticate: Bearer error="insufficient_scope", error_description="The request requires higher privil
```
## API Description
This API is used to verify the SMS or email one-time password (OTP) verification code, get the Access Token and ID Token for login. Before calling this API, you need to call the [API for sending OTP verification code](https://www.tencentcloud.com/document/product/1148/51475) to send a verification code to user.

>? You can set `auto_signup=true` to enable automatic sign-up of users.

## Supported Applications
Web applications, single-page applications (SPA), and mobile applications.

## Request Method
```
POST
```
## Request Path
```
/oauth2/token
```
## Request Content-Type
```
application/json
```

## Sample Requests
#### OTP login by SMS
```
POST /oauth2/token HTTP/1.1
Content-Type: application/json
Host: sample.portal.tencentciam.com

{
  "grant_type" : "http://tencentciam.com/oauth2/grant-type/otp/sms",
  "client_id" : "TENANT_CLIENT_ID",
  "client_secret" : "TENANT_CLIENT_SECRET",
  "auth_source_id" : "MOCK_SMS_OTP_AUTH_SOURCE_ID",
  "phone_number" : "13612345678",
  "otp_token" : "MOCK_OTP_TOKEN",
  "otp" : "123456"
}
```
#### OTP login by email
```
POST /oauth2/token HTTP/1.1
Content-Type: application/json
Host: sample.portal.tencentciam.com

{
  "grant_type" : "http://tencentciam.com/oauth2/grant-type/otp/email",
  "client_id" : "TENANT_CLIENT_ID",
  "client_secret" : "TENANT_CLIENT_SECRET",
  "auth_source_id" : "MOCK_EMAIL_OTP_AUTH_SOURCE_ID",
  "email" : "MOCK_USERNAME@example.com",
  "otp_token" : "MOCK_EMAIL_OTP_TOKEN",
  "otp" : "123456"
}
```

## Request Parameters in JSON Format
| JSON Path | Data Type | Description |
| :------------- | :------- | :----------------------------------------------------------- |
| grant_type | String | <li>OTP login by SMS: `http://tencentciam.com/oauth2/grant-type/otp/sms`</li><li>OTP login by email: `http://tencentciam.com/oauth2/grant-type/otp/email` </li> |
| client_id | String | The `client_id` of the application. This should be the same as that used for sending verification code.           |
| client_secret | String | The `client_secret` of the application. This parameter is required for web applications, yet it is not needed for SPA and mobile applications. |
| auth_source_id | String | The ID of the authentication source for OTP by SMS or email. This should be the same as that used for sending verification code. |
| phone_number | String | The user's mobile number. This should be the same as that used for sending verification code. This parameter is required for OTP login by SMS. |
| email | String | The user's email address. This should be the same as that used for sending verification code. This parameter is required for OTP login by email. |
| otp_token | String | The `otp_token` returned by the server after the verification code is sent.                   |
| otp | String | The OTP verification code received by the user's mobile number or email.                            |
| auto_signup | Boolean | To enable automatic sign-up of users, pass "true". Otherwise, this parameter is not required.        |

## Sample Success Responses
```
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
  "access_token" : "eyJraWQiOiJmZTQ4YTJjYS1lNGU3LTQyMGEtOThjOS01OGM5NmI2NzUwZjIiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJNT0NLX1VTRVJfSUQiLCJhdWQiOiJURU5BTlRfQ0xJRU5UX0lEIiwibmJmIjoxNjQ3NDIwMDM1LCJzY29wZSI6WyJvcGVuaWQiXSwiaXNzIjoiaHR0cHM6XC9cL3NhbXBsZS5wb3J0YWwudGVuY2VudGNpYW0uY29tIiwiZXhwIjoxNjQ3NDIwMzM1LCJpYXQiOjE2NDc0MjAwMzUsImp0aSI6ImMxZmE5Yzk4LThhZjQtNDA1Zi1iOWFhLTdiNTU2MjY1NDljNSJ9.FzvKdLeIgNeYKwQeixIGKX2JPkZ9tJ43fnwuaruLY85RQj9cMedm9eSU4Ft_h7NJkwH-eBTmSybg7174RsQ98yOaW77u2flQwxm0xZCx74kY2dOZOf3YhRJwVLVhocMtLC1NrrP3phJSVfYYzClS_ppTnSHcGZhiVzW57YgolTr0EeuOMucmt1jh_I76kDreo_B5UhV95sRqP_R5FMVBLpGvlAD3TPVCMs3zQETlgHHyq2UE9YBnkNBLK9RzxknRZ0XSnUMxpcPCod4e7Q7S87QqML2S_3AbcmJlPY5q0D-XTqzyjvS2QByUOUQNOX6pEH4Pe7fV6phVrfXh0IenDQ",
  "refresh_token" : "B-72VlkQa3jQNuo9Xbbl-muoh4w7nYu-7Q3Wb-qmPgyftN1CgXPov2aWsOBWeeIOIVHjVxxHxbOa21Oz0CtIgsIz1LMZ_HG7eLxF-qk6hiRcFzPOcSl8PBsCdd3QXaEd",
  "scope" : "openid",
  "id_token" : "eyJraWQiOiJmZTQ4YTJjYS1lNGU3LTQyMGEtOThjOS01OGM5NmI2NzUwZjIiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJNT0NLX1VTRVJfSUQiLCJhdWQiOiJURU5BTlRfQ0xJRU5UX0lEIiwiYXpwIjoiVEVOQU5UX0NMSUVOVF9JRCIsImlzcyI6Imh0dHBzOlwvXC9zYW1wbGUucG9ydGFsLnRlbmNlbnRjaWFtLmNvbSIsImV4cCI6MTY0NzQyMTgzNSwiaWF0IjoxNjQ3NDIwMDM1LCJqdGkiOiI5MGFiMzljMi00NjQzLTQwYTEtODdmOC0yN2Q5ODkzOTExMDQifQ.ZqgRcJae_XEUd1XIbu2_pzdgnJCtEehLoCTTHJhEvewOeEnUlfYkRMrpfZ_hYSVsaWDZy0zdqntWmpmN57eJuw-nfwaUGBUjc1e3KgyvY9jr5vo4zlI5O2NJYYMwP8uwwCFsqWjbNl1cl-dVPu6pIGAvPWBx_Hm1C0vMsPICv61KE7I4bGi_XCSQ--CQjvjzE8ly4I7Z1jCfVl9f4Aybve2HJkuD-m73nZsgluAGOANXvBLcYi1bj4ncXt9Ybk45Gt_vtlCOY9Ab-N6STm4omtKuxyMQUfy7Rv-9RXBuvDFIdDl6tpENxch1N0V027FdtdWk_JOk9mq97rqI-LycPA",
  "token_type" : "Bearer",
  "expires_in" : 299
}
```

## Response Parameters
| Parameter | Data Type | Description |
| :------------ | :------- | :---------------------------------------- |
| access_token | String | OAuth 2.0 Access Token (JWT).            |
| token_type | String | Token type. Fixed value: `Bearer`. |
| expires_in | Number | Validity period of Access Token (unit: sec)             |
| scope | String | Access Token scope.                      |
| refresh_token | String | OAuth 2.0 Refresh Token.                 |
| id_token | String | OpenID Connect (OIDC) ID Token (JSON Web Token, or JWT).                     |

## Sample Error Responses
- `otp_token` is incorrect or has expired.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant",
  "error_description" : "Unknown or expired otp_token"
}
```
- `otp` is incorrect or has expired.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant",
  "error_description" : "Unknown or expired OTP"
}
```
- The parameter used is not the same as the one for sending the verification code. For example, the mobile numbers are different.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_request",
  "error_description" : "Mismatched OTP token and OTP sending parameters"
}
```
- The user corresponding to the mobile number or email address cannot be found. This occurs when automatic sign-up of users is not allowed.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant",
  "error_description" : "User not found"
}
```
- The status of the user corresponding to the mobile number or email address is abnormal. For example, the account is locked or frozen.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant",
  "error_description" : "Abnormal user status"
}
```
- The authentication source is not the preferred one or is not associated with the application.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_auth_source",
  "error_description" : "Auth source and application not associated"
}
```
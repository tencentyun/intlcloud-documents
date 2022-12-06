## API Description
This API is used to sign up a new user. This API is suitable for **automatic application sign-up development scenarios**. If your application uses the Customer Identity Access Management (CIAM) authentication portal, see [Sign up via Authentication Portal](https://www.tencentcloud.com/document/product/1148/51469).

Before calling this API, make sure that the application sign-up process has been configured and enabled. Input parameters of the API need to follow the rules of the application configured for the sign-up process. For example, if the mobile number is set as a authentication attribute and the username as the required general attribute for the sign-up process, the input parameters must contain the mobile number and the username. **If the mobile number is not set as a authentication attribute for sign-up, the input parameters cannot contain the mobile number**.

When the sign-up information contains a mobile number or email address, you need to call the [API for sending one-time password (OTP) verification code](https://www.tencentcloud.com/document/product/1148/51475) to send the verification code to the user.

Password is an optional parameter, which can be set as needed.
- If users only log in via SMS OTP, email OTP or social authentication, no password is required.
- If users are allowed to log in by account and password authentication, a password should be set.

If you need to set a password, make sure that the **authentication source of account and password is associated** in the login process of the application. The API will verify the passed password according to the password policies of the authentication source. If the password does not meet the policy requirements, the sign-up will fail.
>?
>- The user groups cannot be set via this API. Users who has signed up are included in the user group configured in the sign-up process by default.
>- This API does not handle automatic login and identity verification logic. The configurations of automatic login and identity verification in the sign-up process do not take effect on this API.

## Supported Applications
Web applications.

## Request Method
```
POST
```

## Request Path
```
/signup
```

## Request Content-Type
```
application/json
```

## Sample Requests
- Sign up with a username and set a password.
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
- Sign up with an email and an alias and set a password.
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
- Sign up with a mobile number without setting a password.
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

## Request Headers

| Parameter | Description |
| :------------ | :----------------------------------------------------------- |
| Authorization | HTTP `Basic` authentication request header. The format is `Basic <credentials>`, where `Basic` is a fixed string and `<credentials>` is calculated by `base64(url_encode(client_id) + ":" + url_encode( client_secret))`. `Basic` and `<credentials>` are separated by a space. |

## Request Parameters in JSON Format
| JSON Path | Data Type | Description |
| :--------------------- | :------- | :----------------------------------------------------------- |
| username | String | Username. It can contain up to 32 characters of letters, numbers and underscores. It must start with a letter. |
| password | String | User password. The password you set must comply with the policies of the account and password authentication source associated with the application. |
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

## Sample Success Responses of Sign-up
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "sub" : "MOCK_USER_ID"
}
```

## Response Parameters
| Parameter | Data Type | Description |
| :--- | :------- | :------------- |
| sub | String | Unique identifier of the user. |

## Sample Error Responses of Sign-up
- The sign-up process of the application is not enabled.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "misconfigured",
  "error_description" : "Sign up flow of the application is not enabled."
}
```
- The input parameters do not contain the authentication attributes or required general attributes configured in the sign-up process.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_request",
  "error_description" : "Missing required sign-up attribute(s)."
}
```
- The input parameters contain authentication attributes or general attributes that are not configured in the sign-up process.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_request",
  "error_description" : "Unconfigured sign-up attribute(s) found."
}
```
- The input parameters contain unknown attributes.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_request",
  "error_description" : "Unknown attribute(s) found."
}
```
- The username format is invalid.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_username"
}
```
- The username already exists.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "duplicate_username"
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
- A password is passed as an input parameter, but the account and password authentication source is not associated in the application login process.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "misconfigured",
  "error_description" : "No password auth source is associated with the application."
}
```
- The password does not meet the policy requirements.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_password"
}
```
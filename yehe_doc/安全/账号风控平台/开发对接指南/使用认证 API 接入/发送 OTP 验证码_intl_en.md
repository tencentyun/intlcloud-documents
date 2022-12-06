## API Description
This API is used to send SMS or email one-time password (OTP) verification code to users for login, sign-up or user information update.



## Supported Applications
Web applications and machine-to-machine (M2M) applications.

## Request Method
```
POST
```
## Request Path
```
/otp/send
```
## Request Content-Type
```
application/json
```

## Sample Requests
- Send SMS verification code for OTP login by SMS.
```
POST /otp/send HTTP/1.1
Content-Type: application/json
Authorization: Basic VEVOQU5UX0NMSUVOVF9JRDpURU5BTlRfQ0xJRU5UX1NFQ1JFVA==
Host: sample.portal.tencentciam.com

{
  "usage" : "login",
  "phone_number" : "13612345678",
  "auth_source_id" : "MOCK_SMS_OTP_AUTH_SOURCE_ID"
}

```
- Send email verification code for OTP login by email.
```
POST /otp/send HTTP/1.1
Content-Type: application/json
Authorization: Basic Q0xJRU5UXzRfSUQ6Q0xJRU5UXzRfU0VDUkVU
Host: sample.portal.tencentciam.com

{
  "usage" : "login",
  "email" : "MOCK_USERNAME@example.com",
  "auth_source_id" : "MOCK_EMAIL_OTP_AUTH_SOURCE_ID"
}
```
- Send SMS verification code for binding mobile number during sign-up.
```
POST /otp/send HTTP/1.1
Content-Type: application/json
Authorization: Basic Q0xJRU5UXzRfSUQ6Q0xJRU5UXzRfU0VDUkVU
Host: sample.portal.tencentciam.com

{
  "usage" : "signup",
  "phone_number" : "13612345678"
}
```
- Send email verification code for binding email address during sign-up.
```
POST /otp/send HTTP/1.1
Content-Type: application/json
Authorization: Basic Q0xJRU5UXzRfSUQ6Q0xJRU5UXzRfU0VDUkVU
Host: sample.portal.tencentciam.com

{
  "usage" : "signup",
  "email" : "MOCK_USERNAME@example.com"
}
```
- Send email verification code for binding or changing mobile number to update user information.
```
POST /otp/send HTTP/1.1
Content-Type: application/json
Authorization: Basic Q0xJRU5UXzRfSUQ6Q0xJRU5UXzRfU0VDUkVU
Host: sample.portal.tencentciam.com

{
  "usage" : "update_userinfo",
  "phone_number" : "13612345678"
}
```
- Send email verification code for resetting password.
```
POST /otp/send HTTP/1.1
Content-Type: application/json
Authorization: Basic Q0xJRU5UXzRfSUQ6Q0xJRU5UXzRfU0VDUkVU
Host: sample.portal.tencentciam.com

{
  "usage" : "reset_password",
  "email" : "MOCK_USERNAME@example.com"
}
```

## Request Headers
| Parameter | Description |
| :------------ | :----------------------------------------------------------- |
| Authorization | HTTP `Basic` authentication request header. The format is `Basic <credentials>`, where `Basic` is a fixed string and `<credentials>` is calculated by `base64(url_encode(client_id) + ":" + url_encode( client_secret))`. `Basic` and `<credentials>` are separated by a space. |

## Request Parameters in JSON Format
| JSON Path | Data Type | Description |
| :-------- | :------- | :--- |
| usage | String | The use case of the OTP verification code. <li>Enter `login` for OTP login by SMS or email. </li><li>Enter `signup` for user sign-up. </li><li>Enter `update_userinfo` for updating user information. </li><li>Enter `reset_password` for resetting user password. </li><li>If this parameter is not specified, it defaults to login. </li> |
| phone_number | String | The user's mobile number, which should be an 11-digit mobile number of the three major carriers in Chinese mainland. This parameter is required for sending SMS OTP verification code. |
| email | String | The user's email address. This parameter is required for sending email OTP verification code.            |
| auth_source_id | String | The ID of the authentication source for OTP by SMS or email. It can be viewed on the general authentication source list of the console. This parameter is required for OTP login by SMS or email. The length and validity period of the verification code in the authentication source configuration will be used. In other scenarios, this parameter is left empty. A 6-digit verification code will be used by default, which is valid for 60 seconds. |

## Sample Success Responses
The verification code is sent successfully.
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "otp_token" : "MOCK_OTP_TOKEN"
}
```

## Response Parameters
| Parameter | Data Type | Description |
| :-------- | :------- | :------------------------------------------------ |
| otp_token | String | OTP token, which is used in OTP verification. This is valid for 5 minutes. |

## Sample Error Responses
- Incorrect mobile number format.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "malformed_phone_number"
}
```
- Incorrect email address format.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "malformed_email"
}
```
- SMS message can not be sent due to insufficient SMS quota. This occurs when the free quota has been used up. You need to configure the SMS template on the console.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "insufficient_sms_quota"
}
```
- Email can not be sent due to insufficient email quota. This occurs when the free quota has been used up. You need to configure the email template on the console.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "insufficient_email_quota"
}
```
- The email address does not exist or is on the blocklist.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_email"
}
```
- Failed to send the verification code.
```
HTTP/1.1 503 Service Unavailable
Content-Type: application/json;charset=UTF-8

{
  "error" : "temporarily_unavailable",
  "error_description" : "Failed to send OTP. Please try again later."
}
```
- The email address has already been used for sign-up.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
    "error": "email_is_used"
}
```
- The mobile number has already been used for sign-up.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8


{
    "error": "phone_number_is_used"
}
```
- The limit for sending SMS messages to a mobile number is exceeded.
  - If you use the purchased SMS quota, you can modify the message sending limit policy in the [SMS Console](https://console.cloud.tencent.com/smsv2).
  - If you use the free SMS quota, a maximum of 50 SMS messages can be sent to one mobile number every day, and only one SMS message can be sent to one mobile number within 30 seconds.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "sms_rate_limit_exceeded",
  "error_description" : "SMS rate limit exceeded for same phone number"
}
```
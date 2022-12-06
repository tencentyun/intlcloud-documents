## API Description
This API is used to reset the user password. Before calling this API, you need to call the [API for sending one-time password (OTP) verification code](https://www.tencentcloud.com/document/product/1148/51475) to send a verification code to user.

>! The new password must comply with the policies of the account and password authentication source associated with the application. It cannot be the same as the previous N passwords specified in the policy.

## Supported Applications
Web applications, single-page applications (SPA), and mobile applications.

## Request Method
```
POST
```

## Request Path
```
/reset_user_password
```

## Request Content-Type
```
application/json
```
## Sample Requests
```
POST /reset_user_password HTTP/1.1
Content-Type: application/json
Authorization: Basic VEVOQU5UX0NMSUVOVF9JRDpURU5BTlRfQ0xJRU5UX1NFQ1JFVA==
Host: sample.portal.tencentciam.com

{
    "password" : "MOCK_PASSWORD",
    "email" : "MOCK_EMAIL@163.com",
    "email_otp" : "MOCK_EMAIL_OTP",
    "email_otp_token" : "MOCK_EMAIL_OTP_TOKEN"
}
```

## Request Headers
<table>
<thead>
<tr>
<th width="15%">Name</th>
<th width="85%">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">Authorization</td>
<td align="left">HTTP Basic authentication request header. The format is <code>Basic &lt;credentials&gt;</code>, where `Basic` is a fixed string and <code>&lt;credentials&gt;</code> is calculated by <code>base64(url_encode(client_id) + ":" + url_encode(client_secret))</code>. `Basic` and <code>&lt;credentials&gt;</code> are separated by a space. </td>
</tr>
</tbody></table>


## Request Parameters in JSON Format
<table>
<thead>
<tr>
<th width="15%">JSON Path</th>
<th width="15%">Data Type</th>
<th width="70%">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left">client_id</td>
<td align="left">String</td>
<td align="left">The <code>client_id</code> of the application. This should be the same as that used for sending verification code. </td>
</tr>
<tr>
<td align="left">client_secret</td>
<td align="left">String</td>
<td align="left">The <code>client_secret</code> of the application. This parameter is required for web applications, yet it is not needed for SPA and mobile applications. </td>
</tr>
<tr>
<td align="left">password</td>
<td align="left">String</td>
<td align="left">New password.</td>
</tr>
<tr>
<td align="left">email</td>
<td align="left">String</td>
<td align="left">The user's email address. This parameter is required for sending email OTP verification code. </td>
</tr>
<tr>
<td align="left">email_otp_token</td>
<td align="left">String</td>
<td align="left">The <code>otp_token</code> returned by the server after the email verification code is sent. </td>
</tr>
<tr>
<td align="left">email_otp</td>
<td align="left">String</td>
<td align="left">The OTP verification code received by the user's email. </td>
</tr>
<tr>
<td align="left">phone_number</td>
<td align="left">String</td>
<td align="left">The user's mobile number. This parameter is required for sending SMS OTP verification code. </td>
</tr>
<tr>
<td align="left">phone_number_otp_token</td>
<td align="left">String</td>
<td align="left">The <code>otp_token</code> returned by the server after the SMS verification code is sent. </td>
</tr>
<tr>
<td align="left">phone_number_otp</td>
<td align="left">String</td>
<td align="left">The OTP verification code received by the user's mobile phone. </td>
</tr>
</tbody></table>


## Sample Success Responses
The password is reset.
```
HTTP/1.1 200 OK
```

## Sample Error Responses
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
- No user found for the email address.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "user_not_found"
}
```
- The password cannot be reset because the user account is frozen.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "abnormal_user_status",
  "error_description" : "User is frozen."
}
```
- The `email_otp_token` parameter is incorrect or has expired, or Reset parameter value used for resetting is not the same as the one used for sending the verification code. For example, the email addresses are different.
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
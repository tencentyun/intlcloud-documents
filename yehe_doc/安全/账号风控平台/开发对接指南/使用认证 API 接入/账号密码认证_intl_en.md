## API Description
This API is used to verify the username and password and get the Access Token and ID Token for login. This API adopts the Resource Owner Password Credentials mode of the OAuth 2.0 protocol for authentication.
>? The password is passed between the user’s client and the application. Make sure that you use a trusted application to call this API, and properly transmit the password. For example, make sure that the HTTPS protocol is used. We recommend that you use [Login via Authentication Portal](https://www.tencentcloud.com/document/product/1148/51469) first if possible.

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
application/x-www-form-urlencoded
```

## Sample Requests
```
POST /oauth2/token HTTP/1.1
Host: sample.portal.tencentciam.com
Content-Type: application/x-www-form-urlencoded
grant_type=password&client_id=TENANT_CLIENT_ID&client_secret=TENANT_CLIENT_SECRET&auth_source_id=MOCK_USERNAME_PASSWORD_AUTH_SOURCE_ID&username=MOCK_USERNAME&password=MOCK_PASSWORD&scope=openid
```


## Request Parameters
| Parameter | Optional | Description |
| :------------- | :---- | :----------------------------------------------------------- |
| grant_type | false | Fixed value: `password`.                                        |
| client_id | false | The `client_id` of the application. Go to the **[application management page](https://console.cloud.tencent.com/ciam/app-management)** and **select the application**, and then click **Application Configuration** to find the **Client ID**. |
| client_secret | true | The `client_secret` of the application. Go to the **[application management page](https://console.cloud.tencent.com/ciam/app-management)** and **select the application**, and then click **Application Configuration** to find the **client_secret**. <li>This parameter is required for web applications, </li><li>yet it is not needed for SPA and mobile applications. </li> |
| auth_source_id | false | ID of the account and password authentication source. You can view it on the [General Authentication Source page](https://console.cloud.tencent.com/ciam/general-auth-source) on the console. |
| username | false | Username. The authentication source attributes that need to be configured with the account and password authentication source include the username, mobile number, and email address. |
| password | false | User password.                                                   |
| scope | true | This parameter is not required. If this parameter is used, the value should be `openid`.                        |


## Sample Success Responses
#### Authentication successful
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

#### Response parameters
| Parameter | Data Type | Description |
| :------------ | :------- | :---------------------------------------- |
| access_token | String | OAuth 2.0 Access Token (JSON Web Token, or JWT).            |
| token_type | String | Token type. Fixed value: `Bearer`. |
| expires_in | Number | Validity period of Access Token (unit: sec)             |
| scope | String | Access Token scope.                      |
| refresh_token | String | OAuth 2.0 Refresh Token.                 |
| id_token | String | OpenID Connect (OIDC) ID Token (JWT).                     |


## Sample Error Responses
- Incorrect username or password.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant",
  "error_description" : "Wrong username or password"
}
```

- Abnormal user status. For example, the account is locked or frozen.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant",
  "error_description" : "Abnormal user status"
}
```

- An attribute that is not supported by the authentication source is used as the username. For example, an email address is passed as the username, but the authentication source of the account and password does not configure the email address as a authentication source attribute.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant",
  "error_description" : "Unsupported username identifier"
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
## API Description
This API is used to get the Access Token and ID Token for login after the application system gets the `code` returned by the authentication portal through the Proof Key for Code Exchange (PKCE) authorization code mode.

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

client_id=TENANT_CLIENT_ID&grant_type=authorization_code&code=MOCK_CODE&redirect_uri=https%3A%2F%2Fexample.com%2Fcallback&code_verifier=MOCK_CODE_VERIFIER
```


## Request Parameters

| Parameter | Optional | Description |
| :------------ | :---- | :----------------------------------------------------------- |
| client_id | false | The `client_id` of the application. This should be the same as the one used for getting the authorization code.            |
| grant_type | false | Fixed value: `authorization_code`.                              |
| code | false | The authorization code returned.                                     |
| redirect_uri | false | The redirected address after authorization. This should be the same as the one used for getting the authorization code.     |
| code_verifier | false | PKCE code verifier. This should be the same as the `code_verifier` used to generate the `code_challenge`. |


## Sample Success Responses
```
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
  "access_token" : "eyJraWQiOiJkNDliYzUwNS01NTcyLTRlZDYtOWU0OC0zODhjM2Q0NGJiNDYiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJNT0NLX1VTRVJOQU1FIiwiYXVkIjoiVEVOQU5UX0NMSUVOVF9JRCIsIm5iZiI6MTYzNjQ0OTIzMiwic2NvcGUiOlsib3BlbmlkIl0sImlzcyI6Imh0dHBzOlwvXC9URU5BTlQuUE9SVEFMLkRPTUFJTiIsImV4cCI6MTYzNjQ0OTUzMiwiaWF0IjoxNjM2NDQ5MjMyLCJqdGkiOiI0NjkyNTUxMC1mNjY0LTQzNTktODIyYS1jMTdiNTlmNzNhOGUifQ.mmM6iEiGCLIURqaKaJV_LbddUP1i5wCJMJvuasM8i6Wu_Ynix0W_EeghvMcQ94QvLhNYq2KshGQlkl0N5186KCqpHpG6z2ZXbuP35oY4yRFNvhqWOt8drvyxw13aVfehk1_KPLLDgrKGmHTUgxNDvssQq1u6Xd7QxPz0_d0jnaosl78pIO_tV-auGMhYQo6SHHMbFHgJLYBlPUq81eBknqbu8W9Omr4FuDmzlr9VFI4grJ_guxlUuri8lx-C4mRtSbg6bfUYlH7PuAM8bDfaOZ_qhAQ9-KTYF-ZiShDnuJMlVz0u_97ky5kNm_IUOrH6XzWfGL8MboYLagxOHmzNMQ",
  "refresh_token" : "8FuXWpwMZI9oA8ASvCUrqap61N7RvPON6DjWFk-Saiv4dOR8y2tNf9eKf36woAaWYKwW99bpBAQVNWA7P8yM9jiBiGcix42ttYzvRoeMoEBoqYInBgnNMC8jTRTrKDEq",
  "scope" : "openid",
  "id_token" : "eyJraWQiOiJkNDliYzUwNS01NTcyLTRlZDYtOWU0OC0zODhjM2Q0NGJiNDYiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJNT0NLX1VTRVJOQU1FIiwiYXVkIjoiVEVOQU5UX0NMSUVOVF9JRCIsImF6cCI6IlRFTkFOVF9DTElFTlRfSUQiLCJpc3MiOiJodHRwczpcL1wvVEVOQU5ULlBPUlRBTC5ET01BSU4iLCJleHAiOjE2MzY0NTEwMzIsImlhdCI6MTYzNjQ0OTIzMiwianRpIjoiMGMzODNiZTktOGFiNy00YzEwLTg5NWQtMzYwNjgzODg3MmZiIn0.i4Zywl6O5KF7iiivV-8d4Yok7CZr_eQNI8mTS3BkaRCIKiMzXJ55-T55XEonOViUE7s_Z4eMlyInm5-oLmk36NXrkO460LHEwxr8o5BlAnMhC4bd7xX3U3JrQISi6CpJxEn0UXXfJrtHnmR-yxAGNLFkoijM_qV1KWe6Y_OxxKe4FPfM2PwjYACt-XQgs4JsJOQk_UiSnHnvyvbpWTB8ZZriIwwxrNErZxdr09HBWhsQQ5fjJNviSilNLKD5fYYMz0yhl-YxDgMJ7s9tnfpDsNXyX25VpFtjdL4L13d1VAMPs2F5fTFBHX-p9LjoqF2sIJFEBbapgOX5EO-E_v1IFQ",
  "token_type" : "Bearer",
  "expires_in" : 299
}
```


## Response Parameters
| Parameter | Data Type | Description |
| :------------ | :------- | :----------------------------------- |
| access_token | String | OAuth 2.0 Access Token (JWT).       |
| refresh_token | String | OAuth 2.0 Refresh Token.            |
| scope | String | Access Token scope.              |
| id_token | String | OpenID Connect (OIDC) ID Token (JSON Web Token, or JWT).                |
| token_type | String | Token type. Fixed value: `Bearer`. |
| expires_in | Number | Validity period of Access Token (unit: sec)        |

>? Customer Identity Access Management (CIAM) returns ID Token in JWT format. For more information about how to decrypt and verify the ID Token, see the [OpenID Connect document](https://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation). You can also use the development library for decryption and verification. You can get the public key for verification by calling the [API for getting the JWT public key](https://www.tencentcloud.com/document/product/1148/51484).


## Sample Error Responses
- The `client_id` parameter is missing or incorrect.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8
{
  "error" : "invalid_request"
}
```

- The `client_id` is not the same as the one used for getting the authorization code and Token.
```
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8
{
  "error" : "invalid_client"
}
```
- The `grant_type` parameter is incorrect.
```
HTTP/1.1 401 Unauthorized
```
- The `code` parameter is incorrect.
```
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_client"
}
```
- The `code_verifier` parameter is incorrect.
```
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8
{
  "error" : "invalid_client"
}
```
## API Description
This API is used to get the Access Token and ID Token for login after the application system gets the `code` returned by the authentication portal through the normal authorization code mode.

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

client_id=TENANT_CLIENT_ID&client_secret=TENANT_CLIENT_SECRET&grant_type=authorization_code&code=MOCK_CODE&redirect_uri=https%3A%2F%2Fexample.com%2Fcallback
```


## Request Parameters

| Parameter | Optional | Description |
| :------------ | :---- | :----------------------------------------------------------- |
| client_id | false | The `client_id` of the application. This should be the same as the one used for getting the authorization code.            |
| client_secret | false | The `client_secret` of the application. Go to the **[application management page](https://console.cloud.tencent.com/ciam/app-management)** and **select the application**, and then click **Application Configuration** to find the **client_secret**. |
| grant_type | false | Fixed value: `authorization_code`.                              |
| code | false | The authorization code returned.                                     |
| redirect_uri | false | The redirected address after authorization. This should be the same as the one used for getting the authorization code.     |



## Sample Success Responses
```
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
  "access_token" : "eyJraWQiOiJkNDliYzUwNS01NTcyLTRlZDYtOWU0OC0zODhjM2Q0NGJiNDYiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJNT0NLX1VTRVJOQU1FIiwiYXVkIjoiVEVOQU5UX0NMSUVOVF9JRCIsIm5iZiI6MTYzNjQ0OTIzMiwic2NvcGUiOlsib3BlbmlkIl0sImlzcyI6Imh0dHBzOlwvXC9URU5BTlQuUE9SVEFMLkRPTUFJTiIsImV4cCI6MTYzNjQ0OTUzMiwiaWF0IjoxNjM2NDQ5MjMyLCJqdGkiOiJmYmM0NWQ3NS1lYmRjLTQzNjUtOWU0MS01YWM1OTg5ZDdhZTIifQ.SnBaXHhZ0jz3sbo-FPcO91YJn2LqOAuBxWTFRdIzl-PChdh4oXdaxmlWlcaLPU-niBo9TqAAmeocnomkTgt6TS2hp5IOjX8FihshlgVdagQNYM6__Zr5NHw9DH2zEps0AGA_7pyGg9trbcRBkjb2xRLyJpQ5lPkpGiNKA18SfCcsBBoy9E69wrZCZaKo3Y6iHO9v5qxlOTchajR5FI5VDZlxDLX9H3njf3C-KG5NlB7VQZBa0O4TZJm6od_sh8eCmCa5TKF7s5Zhw7JU83JfEh76WKT3rD5uEb4SbFhBGP3hL7Xsj3SJMP7nA4LlQAlINWyFzntAIuJ1VryH3JmQCg",
  "refresh_token" : "Ugvo1lO7Se8vvIPrIOwn_eBe0hoi5-5ynR3H-aFYl0e1Gej-SfUAaBDBXkWmojm_Q7utcpwz_swzLZwGGz_I5wHAkB6iaepCX3LvqZGvt5hmMXDCt3wZY3SnhridZC85",
  "scope" : "openid",
  "id_token" : "eyJraWQiOiJkNDliYzUwNS01NTcyLTRlZDYtOWU0OC0zODhjM2Q0NGJiNDYiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJNT0NLX1VTRVJOQU1FIiwiYXVkIjoiVEVOQU5UX0NMSUVOVF9JRCIsImF6cCI6IlRFTkFOVF9DTElFTlRfSUQiLCJpc3MiOiJodHRwczpcL1wvVEVOQU5ULlBPUlRBTC5ET01BSU4iLCJleHAiOjE2MzY0NTEwMzIsImlhdCI6MTYzNjQ0OTIzMiwianRpIjoiMDBlOWQxMjYtYmJkYi00ZjgzLWI4NTYtNTAyYjI0OWJmNjVmIn0.enLzJ-pJlnKpFCBR0gQc7bJH2GA1q_PpqWNjxJuTE1rWuQzvH9Y0oNNi-Wc1vUQ1u0hPSAC7in4E8vUpWDuDFyXrKWvwNxxj5uyLfFrAc2hnrju0ZUOT58lOqYd0Y48hA6THuxm9aA_EuOHvR3SxIS0cj_O5xJCwvhSqGUldRXGVgB4yMXXvZWkxWm5Q3B_hJc8aZtLpmo76-AKTz2OQouZ5bDE3WD89THuKN4mVxygyyIGTgpuIeyP1x14aTgvNKp2N-HGRoUwCzks_fLMcxmH5vqkI5alMi-XDfG8LWWhObM9j54oShSTpkok51B9VGTTOwbK4ZXeVRI48sCxWmg",
  "token_type" : "Bearer",
  "expires_in" : 299
}
```
>? Customer Identity Access Management (CIAM) returns ID Token in JSON Web Token (JWT) format. For more information about how to decrypt and verify the ID Token, see the [OpenID Connect (OIDC) document](https://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation). You can also use the development library for decryption and verification. You can get the public key for verification by calling the [API for getting the JWT public key](https://www.tencentcloud.com/document/product/1148/51484).


## Response Parameters
| Parameter | Data Type | Description |
| :------------ | :------- | :----------------------------------- |
| access_token | String | OAuth 2.0 Access Token (JWT).       |
| token_type | String | Token type. Fixed value: `Bearer`. |
| expires_in | Number | Validity period of Access Token (unit: sec)        |
| scope | String | Access Token scope.              |
| refresh_token | String | OAuth 2.0 Refresh Token.            |
| id_token | String | OIDC ID Token (JWT).                |

>? Customer Identity Access Management (CIAM) returns ID Token in JWT format. For more information about how to decrypt and verify the ID Token, see the [OpenID Connect document](https://openid.net/specs/openid-connect-core-1_0.html#IDTokenValidation). You can also use the development library for decryption and verification. You can get the public key for verification by calling the [API for getting the JWT public key](https://www.tencentcloud.com/document/product/1148/51484).


## Sample Error Responses
- The `client_id` parameter is missing or incorrect.
```
HTTP/1.1 401 Unauthorized
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
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "unsupported_grant_type",
  "error_description" : "OAuth 2.0 Parameter: grant_type",
  "error_uri" : "https://datatracker.ietf.org/doc/html/rfc6749#section-5.2"
}
```
- The `code` parameter is incorrect.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant"
}
```
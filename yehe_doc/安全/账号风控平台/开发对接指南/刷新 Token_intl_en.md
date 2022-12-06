## API Description
This API is used to get a new `access_token` using `refresh_token`.


## Supported Applications
Web applications, single-page applications (SPA), mobile applications, and machine-to-machine (M2M) applications.

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

client_id=TENANT_CLIENT_ID&client_secret=TENANT_CLIENT_SECRET&grant_type=refresh_token&refresh_token=MOCK_REFRESH_TOKEN
```


## Request Parameters
| Parameter | Optional | Description |
| :------------ | :---- | :----------------------------------------------------------- |
| client_id | false | The `client_id` of the application. This should be the same as the one used for getting the authorization code.             |
| client_secret | false | The `client_secret` of the application. It can be viewed on the basic information page of the application on the Customer Identity Access Management (CIAM) console. |
| grant_type | false | Fixed value: `refresh_token`.                                   |
| refresh_token | false | The `refresh_token` returned when the Token is requested.                        |



## Sample Success Responses
```
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
  "access_token" : "eyJraWQiOiJkNDliYzUwNS01NTcyLTRlZDYtOWU0OC0zODhjM2Q0NGJiNDYiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJNT0NLX1VTRVJOQU1FIiwiYXVkIjoiVEVOQU5UX0NMSUVOVF9JRCIsIm5iZiI6MTYzNjQ0OTIzMSwic2NvcGUiOlsib3BlbmlkIl0sImlzcyI6Imh0dHBzOlwvXC9URU5BTlQuUE9SVEFMLkRPTUFJTiIsImV4cCI6MTYzNjQ0OTUzMSwiaWF0IjoxNjM2NDQ5MjMxLCJqdGkiOiI1YTE4ZjE0MS1lMzQxLTQzMzgtODVkNi1iYjRlNDFhODY3NjUifQ.cP9azxqZW8ELTvr70T2u8S0uxq9fnEKKVh55_6umF0RzBXMtRSeN8bW1uDHzQbYVDfQZQp-vzee35XsfZkS5dYOFQmiOr_uXwd8wdgPvy_8ZHyamY4c4ytZvysx-RDrr6oeHK63lPBrkoC1n_NI6AyZtMZxtxrodggzW593FfqG6vWE7OdPBoeQ8Qk-SEntuReNb60l9f6KYs-H8DJt9f1tYbCe_4ECrxpAbezEyhjVxj_8B72oNCybs3toc1NfZ01ouhGyRIyaDqzKLFFX8QYp-UgZV3N_muUyPNXHhvF4xsiFp_Sf0gSfQ_CYQUoXVs7R_ejSPexqqqYUyXHyzJA",
  "refresh_token" : "MOCK_REFRESH_TOKEN",
  "scope" : "openid",
  "id_token" : "eyJraWQiOiJkNDliYzUwNS01NTcyLTRlZDYtOWU0OC0zODhjM2Q0NGJiNDYiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJNT0NLX1VTRVJOQU1FIiwiYXVkIjoiVEVOQU5UX0NMSUVOVF9JRCIsImF6cCI6IlRFTkFOVF9DTElFTlRfSUQiLCJpc3MiOiJodHRwczpcL1wvVEVOQU5ULlBPUlRBTC5ET01BSU4iLCJleHAiOjE2MzY0NTEwMzEsImlhdCI6MTYzNjQ0OTIzMSwianRpIjoiMDEzYmFiMzktZjkxOC00NDhmLWEzOTYtY2U3N2VlZmZkYjM3In0.M_k7_RnA3E9ptcunBhSSZkxxqqHZhH7PIMn0QQoJGhJ0nja1ZxdMwhEMBmQDZ-cDNaWNUGFT3XZkAsJNBF06g69kAu_gMzRKeGIgCUrQUO_Z1DNoec6Q6oPg3bV5JzYtNjjySEeYrlKxG0PpY3L0uRjpQFXXL6vpm9n4LXz81gsmZiC0JAfJ-n7oDH6QJ8AmfWWJZMs2qobFXsKaFqwBehXFki5qTy8MLxkHMuW-kc4IK0gadlrvic3MRsy3qgfPnwHUfCLb7Ky77EPGXGwFbNzAYGtlimCe-ZN498RatwejTXptiqkBqUhaS7QqdEcI0etAd_4J2DmJYwcXJCFwSg",
  "token_type" : "Bearer",
  "expires_in" : 299
}
```

## Response Parameters
| Parameter | Data Type | Description |
| :------------ | :------- | :-------------------------------------- |
| access_token | String | The refreshed OAuth 2.0 Access Token (JSON Web Token, or JWT). |
| refresh_token | String | The refreshed OAuth 2.0 Refresh Token.      |
| scope | String | Access Token scope.                 |
| id_token | String | The refreshed OpenID Connect (OIDC) ID Token (JWT).          |
| token_type | String | Token type. Fixed value: `Bearer`.     |
| expires_in | Number | Validity period of Access Token (unit: sec)           |


## Sample Error Responses
The `refresh_token` parameter is incorrect.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_grant"
}
```
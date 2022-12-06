## API Description
This API is used to get an Access Token using the OAuth client credentials (`client_credentials`).

## Supported Applications
Web applications and machine-to-machine (M2M) applications.

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

grant_type=client_credentials&client_id=TENANT_CLIENT_ID&client_secret=TENANT_CLIENT_SECRET&scope=identity_proofing
```


## Request Parameters
| Parameter | Optional | Description |
| :------------ | :---- | :----------------------------------------------------------- |
| grant_type | false | Fixed value: `client_credentials`.                              |
| client_id | false | The `client_id` of the application. Go to the **[application management page](https://console.cloud.tencent.com/ciam/app-management)** and **select the application**, and then click **Application Configuration** to find the **Client ID**. |
| client_secret | false | The `client_secret` of the application. Go to the **[application management page](https://console.cloud.tencent.com/ciam/app-management)** and **select the application**, and then click **Application Configuration** to find the **client_secret**. |
| scope | true | The `scope` used to apply for authorization. Multiple `scope` values are separated by spaces.          |




## Sample Success Responses
```
HTTP/1.1 200 OK
Content-Type: application/json;charset=UTF-8

{
  "access_token" : "eyJraWQiOiJmOTY5NGQ5My1kNTQxLTQ5ODUtODhkYy00MjIyOTg3MzAwOGUiLCJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiJURU5BTlRfQ0xJRU5UX0lEIiwiYXVkIjoiVEVOQU5UX0NMSUVOVF9JRCIsIm5iZiI6MTY0MDU4ODgyOCwic2NvcGUiOlsiaWRlbnRpdHlfcHJvb2ZpbmciXSwiaXNzIjoiaHR0cHM6XC9cL3NhbXBsZS5wb3J0YWwudGVuY2VudGNpYW0uY29tIiwiZXhwIjoxNjQwNTg5MTI4LCJpYXQiOjE2NDA1ODg4MjgsImp0aSI6Ijk5MzliYzNmLTVlZGYtNDZjMy04ZjVjLTJiMWRjMWFjZmE5MCJ9.D8khbU3BkWTHD6sRTY9M_bbRq7AF4MGina2S1ycFA2HOUo-k_P_f81V4fP1DLO7n-1_5em_Dmxo768wsFcvUIYWRlSLh91kXPTyBV5mHt6IZRnT3eMpqTiMKC_ubzUc_7DSpE8-99-CpfrQ19hcpMwkoLYh1dwYjUJB6xyZPzqlezrHy4unUHLTpyjGeecgNNLUScY9W0diGxVnbsMuTW7T00OsltNoJj11qtOllbh5kd1B4umvA3UJpGucVMZQ2YTvltHyDBefWabP4ektzktAwDTALGIu1EsQfb5j9Rru3R0L0nAvjT8HiIqthLvvMdkjXAW983zj0yCPe3GqF3g",
  "scope" : "identity_proofing",
  "token_type" : "Bearer",
  "expires_in" : 299
}
```


## Response Parameters
| Parameter | Data Type | Description |
| :----------- | :------- | :---------------------------------------- |
| access_token | String | Access Token (JSON Web Token, or JWT).                      |
| token_type | String | Token type. Fixed value: `Bearer`. |
| expires_in | Number | Validity period of Access Token (unit: sec)             |
| scope | String | Access Token scope.                   |

>？ The Refresh Token is not included in the response for client credentials mode. When the Access Token expires, the application calls this API again to get a new Access Token.


## Sample Error Responses
- The application does not exist or is not enabled; or the verification of the application key failed.
```
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_client"
}
```

- The application does not have permission to use `client_credentials` mode to get the Token.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "unauthorized_client"
}
```

- Incorrect `scope` parameter or no permission.
```
HTTP/1.1 400 Bad Request
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_scope"
}
```
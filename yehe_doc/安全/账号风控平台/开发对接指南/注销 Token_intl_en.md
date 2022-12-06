## API Description
This API is used to revoke the OAuth 2.0 Token. If an `access_token` is passed, only the `access_token` will be revoked. If a `refresh_token` is passed, both the `refresh_token` and its associated `access_token` will be revoked.


## Supported Applications
Web applications, single-page applications (SPA), mobile applications, and machine-to-machine (M2M) applications.

## Request Method
```
POST
```

## Request Path
```
/oauth2/revoke
```

## Request Content-Type
```
application/x-www-form-urlencoded
```

## Sample Requests
```
POST /oauth2/revoke HTTP/1.1
Host: sample.portal.tencentciam.com
Content-Type: application/x-www-form-urlencoded

client_id=TENANT_CLIENT_ID&client_secret=TENANT_CLIENT_SECRET&token=MOCK_ACCESS_TOKEN
```


## Request Parameters
| Parameter | Optional | Description |
| :------------ | :---- | :----------------------------------------------------------- |
| client_id | false | The `client_id` of the application. This should be the same as the one used for getting the authorization code and Token. |
| client_secret | false | The `client_secret` of the application. It can be viewed on the basic information page of the application on the Customer Identity Access Management (CIAM) console. |
| token | false | The value of `access_token` or `refresh_token`.                         |


## Sample Success Responses
```
HTTP/1.1 200 OK
```

## Sample Error Responses
The `client_id` is not the same as the one used for initiating login and getting the Token.
```
HTTP/1.1 401 Unauthorized
Content-Type: application/json;charset=UTF-8

{
  "error" : "invalid_client"
}
```
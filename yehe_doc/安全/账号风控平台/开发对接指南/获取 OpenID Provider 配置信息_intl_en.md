## API Description
This API is used to get the configurations of the OpenID Connect (OIDC) authorization server for simplified local configurations. For more information about the configurations, see [OpenID Connect Discovery](https://openid.net/specs/openid-connect-discovery-1_0.html).


## Supported Applications
Web applications, single-page applications (SPA), mobile applications, and machine-to-machine (M2M) applications.

## Request Method
```
GET
```
## Request Path
```
/.well-known/openid-configuration
```

## Sample Requests
```
GET /.well-known/openid-configuration HTTP/1.1
Host: sample.portal.tencentciam.com
```

## Sample Success Responses
```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "issuer" : "https://sample.portal.tencentciam.com",
  "authorization_endpoint" : "https://sample.portal.tencentciam.com/oauth2/authorize",
  "token_endpoint" : "https://sample.portal.tencentciam.com/oauth2/token",
  "token_endpoint_auth_methods_supported" : [ "client_secret_basic", "client_secret_post" ],
  "jwks_uri" : "https://sample.portal.tencentciam.com/oauth2/jwks",
  "response_types_supported" : [ "code" ],
  "grant_types_supported" : [ "authorization_code", "client_credentials", "refresh_token" ],
  "subject_types_supported" : [ "public" ],
  "id_token_signing_alg_values_supported" : [ "RS256" ],
  "scopes_supported" : [ "openid" ]
}
```

## Response Parameters
| Parameter | Data Type | Description |
| :------------------------------------ | :------- | :------------------------------------------- |
| issuer | String | OIDC issuer.                                |
| authorization_endpoint | String | The URL of the OAuth 2.0 authorization endpoint.               |
| token_endpoint                        | String   | The URL of the OAuth 2.0 token endpoint.            |
| jwks_uri | String | The URL of the JSON Web Token (JWT) public key.                    |
| grant_types_supported | Array | Supported OAuth 2.0 Grant Type values.                |
| response_types_supported | Array | Supported OAuth 2.0 Response Type values. |
| token_endpoint_auth_methods_supported | Array | The authentication methods supported by the OAuth 2.0 token endpoint.    |
| subject_types_supported | Array | Supported OIDC Subject Identifier Type values.        |
| id_token_signing_alg_values_supported | Array | Supported JSON Web Signature (JWS) algorithms.                        |
| scopes_supported | Array | Supported OAuth 2.0 scope values.                     |
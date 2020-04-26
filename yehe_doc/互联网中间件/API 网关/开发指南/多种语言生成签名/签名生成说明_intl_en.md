## Precautions

- If you select key pair authentication when creating an API, the service where the API resides needs to be published, the release environment needs to be bound to a usage plan, and the usage plan needs to be bound to a key pair. Then, the corresponding key pair will be used to generate signing information to authenticate API access requests.
- For a `query` that contains Chinese characters and spaces, the request body should URL-encode the value with UTF-8.
- When a signature is calculated through parameters, the value before encoding should be signed. URL-encoded strings cannot be signed. Please URL-encode the `query` and `body` values after signing.

## Client Error Codes
| Error Code | Status Code | Description | Solution |
|--|---|---|---|
|HMAC signature cannot be verified, a validate authorization header is required|401| The request did not carry the `Authorization` field. | Please construct this field as instructed in the signature demo for the applicable programming language. |
|authorization headers is invalidate|403| The format of the `Authorization` field in the request is incorrect. | Please construct this field as instructed in the signature demo for the applicable programming language. |
|id or signature missing|403| The ID or `signature` field is missing in the `Authorization` field of the request. | Please construct this field as instructed in the signature demo for the applicable programming language. |
|HMAC signature cannot be verified, a valid $header header is required|403| The `headers` field in the `Authorization` field of the request cannot be found in the request header.	| Please construct this field as instructed in the signature demo for the applicable programming language. |
|HMAC signature cannot be verified, a valid date header is required|403| The `Authorization` of the request must use the `date` field as one of the authentication fields. | Please construct this field as instructed in the signature demo for the applicable programming language. |
|Found no validate usage plan|403| Request authentication failed, because the API needs authentication, but the API is not bound to a usage plan. | Please disable API authentication or bind a usage plan to the release environment of the API and bind the key pair to the usage plan. |
|HMAC signature cannot be verified|403| Request authentication failed, because the `Key ID` in the `Authorization` field is not bound to the release environment of the API, the `Key ID` is invalid, or the `Key` is disabled. | Please check whether the key pair is available and bound to the corresponding usage plan/release environment. |
|HMAC signature does not match|403| Request authentication failed, because the calculated HMAC value does not match. Please check and calculate again. | The calculated HMAC value is incorrect. Please construct this field as instructed in the signature demo for the applicable programming language. |
|Not Found Host|404	| The request does not have the `Host` field.	| The request should have the `host` field, whose value should be the server's domain name in string type. |
|Get Host Fail|404| The value of the `host` field in the request is not in string type. | Please change the value of the `Host` field to string type. |
|Could not support method|404| The request method type is not supported. | Please check whether the request method is valid. |
|There is no api match host[$host]|404| Request server domain name/address not found. | Please check whether the request address is correct. |
|There is no api match env_mapping[$env_mapping]|404| The `env_mapping` field after the custom domain name is incorrect. | Please check whether the `env_mapping` configured for the bound custom domain name is the same as the one you entered. |
|There is no api match default env_mapping[$env_mapping]|404| The value of the `env_mapping` field after the default domain name should be `test/prepub/release`. | The value of the `env_mapping` field after the default domain name should be `test/prepub/release`. |
|There is no api match uri[$uri]|404| The API that matches the URI is not found in the service corresponding to the request address. | Please check whether the entered URI is correct. |
|There is no api match method[$method]|404| The API corresponding to the request address plus URI does not support the request method. | Please check whether the request method is correct. |
|"Not allow use HTTPS protocol or Not allow use HTTP protocol"|404| The service corresponding to the requested address does not support the HTTP protocol type. | Please check whether the request protocol type is correct. |
|req is cross origin, api $uri need open cors flag on qcloud apigateway.|429| This is a cross-origin request, but the corresponding API has not enabled cross-origin access. | Please enable cross-origin access for the API. |

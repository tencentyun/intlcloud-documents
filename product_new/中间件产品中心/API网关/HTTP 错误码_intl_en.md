When users call the API Gateway, they may encounter the following common HTTP error codes:

| Error Code|    Log Message  | Description                                                         |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 401    | HMAC apikey is invalid for API.                              | APIKey is not bound to this API.                                     |
| 401    | HMAC signature cannot be verified, a valid x-date header is required for HMAC Authentication. | HMAC verification does not include x-date in the header, or the HMAC value is invalid.  |
| 401    | HMAC signature cannot be verified, the x-date header is out of date for HMAC Authentication. | x-date timestamp timeout, default is 900s.                              |
| 401    | HMAC signature cannot be verified, a valid date or x-date header is required. |  If there is no x-date, the header contains date.                     |
| 401    | HMAC id or signature missing.                                | Authorization ID or signature field is missing.                |
| 401    | HMAC do not support multiple HTTP header.                    | Header with multiple values is not supported.                         |
| 401    | HMAC signature cannot be verified, a valid xxx header is required. | xxx header is missing in the request.                                       |
| 401    | HMAC algorithm xxx not supported.                            | HMAC algorithm does not support xxx, which currently supports hmac-sha1, hmac-sha256, hmac-sha384, and hmac-sha512.  |
| 401    | HMAC authorization format error.                             | Authorization format error.                                     |
| 401    | HMAC authorization headers is invalidate.                    | Authorization lacks sufficient parameters, please refer to the [relevant documentation](https://intl.cloud.tencent.com/document/product/628/11819#.E6.9C.80.E7.BB.88.E5.8F.91.E9.80.81.E5.86.85.E5.AE.B9). |
| 401    | HMAC signature cannot be verified.                           | Unable to verify signature, possibly because APIKey cannot be recognized. This usually happens when APIKey is not bound to this service or API. |
| 401    | HMAC signature does not match.                               | Signature does not match.                                               |       
| 401    | Oauth call authentication server fail.                       | Invoking verification server failed.                                         |
| 401    | Oauth found no related Oauth api.                            |  As the associated Oauth verification API is not found, id_token cannot be verified.           |
| 401    | Oauth miss Oauth id_token.                                   | id_token is missing in request.                                          |
| 401    | Oauth signature cannot be verified, a validate authorization header is required. | No verification header.                                               |
| 401    | Oauth authorization header format error.                     | Oauth header format error.                                         |
| 401    | Oauth found no authorization header.                         | No verification header found.                                           |
| 401    | Oauth found no id_token.                                     | No id_token found.                                          |
| 401    | Oauth id_token verify error.                                 | JWT-formatted id_token validation failed.                               |
| 403    | Found no validate usage plan.                                | No  usage plan found, access denied (an error that may occur when enabling usage plan).  |
| 403    | Cannot identify the client IP address, unix domain sockets are not   supported. | Unable to identify source IP.                                              |
| 403    | Endpoint IP address is not allowed.                          |  Backend IP that is not allowed to be accessed.                                           |
| 403    | Get xxx params fail.                                         |  An error occurred while getting parameter from request.                                      |
| 403    | need header Sec-WebSocket-Key.                               |  Header Sec-WebSocket-Key is missing in request, which will be checked by the API that has configured websocket. |
| 403    | need header Sec-WebSocket-Version.                               |  Header Sec-WebSocket-Version is missing in request, which will be checked by the API that has configured websocket. |
| 403    | header xxx is required.                                      | Header xxx is missing in request.                                    |
| 403    | path variable xxx is required.                               | Path configuration `{xxx}` is configured, but it does not match the path of request.        |
| 403    | querystring xxx is required.                                 | querystring xxx is missing in request.                               |
| 403    | req content type need application/x-www-form-urlencoded.     | The request configured with the body parameter must be in table format.                       |
| 403    | body param xxx is required.                                  | Body parameter xxx is missing in request.                                 |
| 404    | Not found micro service with key.                            | Microservice not found.                                       |
| 404    | Not Found Host.                                              |  Request has host field, host field value needs to be filled in with server's string type domain name. |
| 404    | Get Host Fail.                                               | Request host field value is not string type.                   |
| 404    | Could not support method.                                    | This request method type is not supported.                                    |
| 404    | There is no api match host[$host].                           | Request server domain name/address not found.                                  |
| 404    | There is no api match env_mapping[$env_mapping].             | env_mapping field after the custom domain name is incorrect.                        |
| 404    | There is no api match default env_mapping[$env_mapping].     |  env_mapping field after the default domain name needs to be test/prepub/release.   |
| 404    | There is no api match uri[$uri].                             | The API that matches URI is not found in the service related to the request address.          |
| 404    | Not allow use HTTPS protocol or Not allow use HTTP protocol. | Service related to the request address does not support HTTP protocol type.             |
| 404    | Found no api.                                                | Request did not match API.                                         |
| 426    | Not allow use HTTPS protocol.                                | HTTPS protocol not allowed.                                        |
| 426    | Not allow use HTTPS protocol.                                | HTTP protocol not allowed.                                        |
| 426    | Not allow use HTTPS protocol.                                | xxx protocol not allowed.                                        |
| 429    | API rate limit exceeded.                                     | Request rate exceeds rate limit, view request header for current rate value.        |
| 429    | API quota exceeded.                                          |  Configuration quota reached and remaining quotas can be viewed through request header.              |
| 429    | req is cross origin, api $uri need open cors flag on qcloud   apigateway. | This is a cross-domain request, but API has not enabled cross-domain switching.            |
| 481    | API config error.                                            | API configuration error.                                               |
| 481    | TSF config error.                                            | TSF configuration error.                                           |
| 481    | Get location of micro service info fail.                     | Microservice name and namespace are not configured to get location.                |
| 481    | Only support the map_from like method.req.{path}.{}.         |  Microservice name and namespace are configured to get location, but the location format is invalid.     |
| 481    | Found no valid cors config.                                  | CORS configuration error.                                              |
| 481    | Oauth public key error.                                      | Public key certificate configuration error.                                         |
| 481    | Oauth id_token location forbidden.                           | forbidden id_token storage location.                                 |
| 481    | Oauth found no oauth config.                                 | Oauth configuration not found.                                        |
| 481    | Oauth found no public key.                                   | Public key not found.                                               |
| 481    | Mock config error.                                           | Mock configuration error.                                            |
| 499    | Client closed connetion.                                     | Client closed connection.                                         |
| 500    | Error occurred during query params.                          | Query parameter error.                                         |
| 500    | Internal Server Error.                                       | 1. Other APIGW internal logic error. <br>2. If API is proxy type, accessing the backend address without access permission will also report this error. |
| 502    | Bad Gateway.                                                 | Backend service connection error, possible reasons: <br>1. Backend denied the service, and the 502 error occurred for all requests. <br>2. Backend load is too high, and the 502 error occurred for some of request responses.  |
| 504    | Gateway Time-out.                                            | Backend server connection timeout.                                         |

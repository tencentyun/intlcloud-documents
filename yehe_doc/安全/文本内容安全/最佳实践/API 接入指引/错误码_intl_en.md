## Common Error Codes

| Error Code | Description |
| :------------------------------------ | :----------------------------------------------------------- |
| ActionOffline                         | The API is deactivated.                                                   |
| AuthFailure.InvalidAuthorization      | The `Authorization` in the request headers doesn't meet Tencent Cloud standards.                  |
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | [MFA failure](https://intl.cloud.tencent.com/document/product/378/12036). |
| AuthFailure.SecretIdNotFound | The key does not exist. Check whether the key has been deleted or disabled in the console, and if not, check whether the key is correctly entered. Note that there shall be no space before or after the key. |
| AuthFailure.SignatureExpire | Signature expired. The timestamp and server time cannot differ by more than five minutes. Make sure that your current local time matches the standard time. |
| AuthFailure.SignatureFailure | Invalid signature. The signature calculation is incorrect. Make sure that you have followed the signature calculation steps as described in the signature algorithm document in the calling method. |
| AuthFailure.TokenFailure | Incorrect token. |
| AuthFailure.UnauthorizedOperation | The request is not authorized. For more information, see the authentication description in the [CAM documentation](https://intl.cloud.tencent.com/document/product/1121/43756). |
| DryRunOperation | DryRun Operation. It means that the request would have succeeded, but the DryRun parameter was used. |
| FailedOperation | The operation failed. |
| InternalError | Internal error. |
| InvalidAction | The API does not exist. |
| InvalidParameter                      | Incorrect request parameter (such as parameter format and type). |
| InvalidParameterValue | Invalid parameter value. |
| InvalidRequest                        | The multipart format of the request body is incorrect.                              |
| IpInBlacklist                         | The IP address is in the blocklist.                                            |
| IpNotInWhitelist                      | The IP address is not in the allowlist.                                          |
| LimitExceeded | The quota limit is exceeded. |
| MissingParameter | A parameter is missing. |
| NoSuchProduct                         | The product does not exist.                                                   |
| NoSuchVersion | The API version does not exist. |
| RequestLimitExceeded | The request rate limit is exceeded. |
| RequestLimitExceeded.IPLimitExceeded  | The IP frequency limit is exceeded.                                                      |
| RequestLimitExceeded.UinLimitExceeded | The frequency limit of the root account is exceeded.                                                   |
| RequestSizeLimitExceeded              | The request packet size exceeds the limit.                                           |
| ResourceInUse | The resource is in use. |
| ResourceInsufficient | Insufficient resource. |
| ResourceNotFound | The resource does not exist. |
| ResourceUnavailable | The resource is unavailable. |
| ResponseSizeLimitExceeded             | The response packet size exceeds the limit.                                           |
| ServiceUnavailable                    | The service is temporarily unavailable.                                           |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter                      | Unknown parameter. An undefined parameter can cause an error.                 |
| UnsupportedOperation | Unsupported operation. |
| UnsupportedProtocol | Unsupported HTTP(S) request protocol. Only GET and POST requests are supported. |
| UnsupportedRegion | Unsupported region. |

## Business Error Codes

| Error Code | Description |
| :--------------------------------------- | :--------------------------------------------- |
| InternalError.ErrTextTimeOut             | The request timed out.                                       |
| InvalidParameter.ErrAction               | Incorrect action.                                  |
| InvalidParameter.ErrTextContentLen       | The text in the request is too long.                             |
| InvalidParameter.ErrTextContentType      | The text type is incorrect. The text must be Base64-encoded.               |
| InvalidParameterValue.ErrTextContentLen  | The text in the request exceeds the length limit.                         |
| InvalidParameterValue.ErrTextContentType | The format of the text in the request is incorrect. The text must be Base64-encoded. |
| UnauthorizedOperation.Unauthorized       | The API is not authorized.                               |
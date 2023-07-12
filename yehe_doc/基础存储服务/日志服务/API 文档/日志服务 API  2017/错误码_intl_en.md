## Feature Description

This document describes the error codes and error messages returned when errors occur with the API requests. You can identify the problem based on `StatusCode` and `Body` of HTTP. The format of `Body` is as follows:

```
{
    "errorcode" : "<ErrorCode>",
    "errormessage" : "<ErrorMessage>"
}
```

## Error Codes

| HTTP Status Code | Error Code | Error Message |
| ------------------------- | -------------------- | ------------------------------------------------------------ |
| 400                       | InvalidAuthorization | Invalid signature string format.                                             |
| 400                       | InvalidCompressType  | The specified `x-cls-compress-type` is not supported.                            |
| 400                       | InvalidContent       | Message body error due to decompression or parse failure.                             |
| 400                       | InvalidContentType   | The specified `Content-Type` is not supported.                                   |
| 400                       | InvalidParam         | Required parameter is missing or invalid.                               |
| 400                       | MissingAgentIp       | Missing `x-cls-agent-ip`.                                          |
| 400                       | MissingAgentVersion  | Missing `x-cls-agent-version`.                                     |
| 400                       | MissingAuthorization | Missing `Authorization`.                                           |
| 400                       | MissingContent       | Empty message body.                                                 |
| 400                       | MissingContentType   | Missing `Content-Type`.                                            |
| 400                       | TopicClosed          | The collection feature has been disabled for the specified log topic.                               |
| 400                       | IndexRuleEmpty       | The specified log topic has no index rule configured.                             |
| 400                       | LogsetNotEmpty       | The specified logset is not empty and contains log topics.                               |
| 400                       | SyntaxError          | Search syntax error.                                                 |
| 400                       | LogsetEmpty          | The specified log topic is empty and contains no log topics.                         |
| 400                       | LimitExceeded           | The number of concurrent search requests exceeded the upper limit.                         |
| 400                        | InvalidParameterValue | Incorrect parameter value. |
| 400                        | MissingParameter | Some function parameters are missing. |
| 400                        | UnknownParameter | Unknown function parameters. |
| 400                        | InvalidParameter | Function parameter error. |
| 400                        | UnsupportedRegion | The region is not supported. |
| 400                        | RequestLimitExceeded | The number of function requests exceeds the system limit. |
| 400                        | NoSuchVersion | Incorrect SCF version. |
| 400                        | ResourceNotFound | No function found. |
| 401                       | AuthFailure.SecretIdNotFound | The key does not exist. Check whether the key has been deleted or <br>disabled in the console, and if not, check if the key is correctly entered. Note that there should be no space before or after the key. |
| 401                       | AuthFailure.SignatureFailure         | Incorrect signature due to errors in signature calculation.<br>Check the signature calculation process against the calling method documentation.                    |
| 401                       | AuthFailure.SignatureExpire         | Signature expired.                                 |
| 401                       | AuthFailure.MFAFailure         | MFA error.                                 |
| 401                       | AuthFailure.UnauthorizedOperation         | Unauthorized request. For more information about authentication, see the [CAM documentation](https://intl.cloud.tencent.com/zh/document/product/598).  |
| 401                       | AuthFailure.InvalidSecretId         | Invalid key (not a TencentCloud API key).                                 |
| 401                       | AuthFailure.TokenFailure         | Token error.                                 |
| 401                       | AuthFailure.Unauthorized         | Internal authentication error.                                 |
| 403                       | LogsetExceed         | The number of logsets exceeds the upper limit. Up to 20 logsets are supported.                              |
| 403                       | LogSizeExceed        | The size of the submitted logs exceeds the upper limit. The maximum size supported is 5 MB.                            |
| 403                       | MachineGroupExceed   | The number of machine groups exceeds the upper limit. Up to 200 machine groups are supported.                                |
| 403                       | NotAllowed           | This operation is not allowed.                                                 |
| 403                       | TopicExceed          | The number of log topics exceeds the upper limit. Up to 10 log topics are supported.                               |
| 403                       | ShipperExceed        | The number of shipping rules exceeds the upper limit. Up to 10 shipping rules are supported.                               |
| 403 | TaskReadOnly | Only failed shipping tasks can be restarted. Tasks in other states cannot be modified. |
| 403                       | AccountArrears          | The account has overdue payment.             |
| 403                       | ServiceNotActivated          | The CLS service is not activated.             |
| 404                       | CursorNotExist       | No downloadable logs exist in the specified location.                                 |
| 404                       | TaskNotExist         | The specified shipping task does not exist.                                         |
| 404                       | IndexNotExist        | The specified index rule does not exist.                                         |
| 404                       | LogsetNotExist       | The specified logset does not exist.                                           |
| 404                       | MachineGroupNotExist | The specified machine group does not exist.                                           |
| 404                       | ShipperNotExist      | The specified shipping rule does not exist.                                         |
| 404                       | TopicNotExist        | The specified log topic does not exist.                                         |
| 404                       | ConsumerNotExist     | The specified log topic has no consumption task.                                 |
| 404                       | DeliverFunctionNotExist | The shipping task does not exist. |
| 405                       | NotSupported         | Unsupported operation.                                                 |
| 409                       | IndexConflict        | This index rule already exists.                                         |
| 409                       | LogsetConflict       | This logset already exists.                                           |
| 409                       | MachineGroupConflict | This machine group already exists.                                           |
| 409                       | ShipperConflict      | This shipping rule already exists.                                         |
| 409                       | TopicConflict        | This log topic already exists.                                        |
| 409                       | ConsumerConflict     | This consumption task of the log topic already exists.                                     |
| 409                       | DeliverFunctionConflict | The same shipping task already exists. |
| 429                       | SpeedQuotaExceed     | Requests are sent too frequently.                                                 |
| 500 | InternalError | Internal error. |

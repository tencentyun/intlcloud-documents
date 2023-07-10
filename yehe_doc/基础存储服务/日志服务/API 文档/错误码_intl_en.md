## Feature

This document describes the error code and corresponding error message returned when a request fails. You can determine the problem based on the HTTP `StatusCode` and `Body`. The format of `Body` is as follows:

```
{
    "errorcode" : "<ErrorCode>",
    "errormessage" : "<ErrorMessage>"
}
```

## Error Code List

| HTTP Status Code | Error Code | Error Message |
| ------------------------- | -------------------- | ------------------------------------------------------------ |
| 400                       | InvalidAuthorization | Invalid signature string format                                             |
| 400                       | InvalidCompressType  | The specified `x-cls-compress-type` is not supported                            |
| 400                       | InvalidContent       | Message body error due to decompression or parse failure                             |
| 400                       | InvalidContentType   | The specified  `Content-Type` is not supported                                   |
| 400                       | InvalidParam         | Required parameter is missing or invalid                               |
| 400                       | MissingAgentIp       | Missing `x-cls-agent-ip`                                          |
| 400                       | MissingAgentVersion  | Missing `x-cls-agent-version`                                     |
| 400                       | MissingAuthorization | Missing `Authorization`                                           |
| 400                       | MissingContent       | Empty message body                                                 |
| 400                       | MissingContentType   | Missing `Content-Type`                                            |
| 400                       | TopicClosed          | The collection feature has been disabled for the specified log topic                               |
| 400                       | IndexRuleEmpty       | The specified log topic has no index rule configured                             |
| 400                       | LogsetNotEmpty       | The specified logset is not empty and contains log topics                               |
| 400                       | SyntaxError          | Search syntax error                                                 |
| 400                       | LogsetEmpty          | The specified log topic is empty and contains no log topics                         |
| 401                       | AuthFailure.SecretIdNotFound | Key does not exist. Check if the key has been deleted or disabled in the console, and if not, check if the key is correctly entered. <br>Note that there should be no space before or after the key. |
| 401                       | AuthFailure.SignatureFailure         | Incorrect signature due to errors in signature calculation.<br>Check the signature calculation process against the calling method documentation                    |
| 401                       | AuthFailure.SignatureExpire         | Expired signature                                 |
| 401                       | AuthFailure.MFAFailure         | MFA error                                 |
| 401                       | AuthFailure.UnauthorizedOperation         | Unauthorized request. For more information about the authentication, see the [CAM](https://intl.cloud.tencent.com/zh/document/product/598) documentation |
| 401                       | AuthFailure.InvalidSecretId         | Invalid key (it is not a TencentCloud API key)                                 |
| 401                       | AuthFailure.TokenFailure         | token error                                 |
| 401                       | AuthFailure.Unauthorized         | Internal authentication error                                 |
| 403                       | LogsetExceed         | The number of logsets exceeds the upper limit. Up to 20 logsets are supported                              |
| 403                       | LogSizeExceed        | The size of the submitted logs exceeds the upper limit. The maximum size supported is 5 MB                            |
| 403                       | MachineGroupExceed   | The number of server groups exceeds the upper limit. Up to 200 server groups are supported                                |
| 403                       | NotAllowed           | This operation is not allowed                                                 |
| 403                       | TopicExceed          | The number of log topics exceeds the upper limit. Up to 10 log topics are supported                               |
| 403                       | ShipperExceed        | The number of shipping rules exceeds the upper limit. Up to 10 shipping rules are supported                               |
| 403 | TaskReadOnly | Only failed shipping tasks can be restarted. Tasks in other statuses cannot be modified |
| 403                       | AccountArrears          | The account has overdue payment             |
| 403                       | ServiceNotActivated          | The CLS service is not activated             |
| 404                       | CursorNotExist       | There are no downloadable logs in the specified location                                 |
| 404                       | TaskNotExist         | The specified shipping task does not exist                                         |
| 404                       | IndexNotExist        | The specified index rule does not exist                                         |
| 404                       | LogsetNotExist       | The specified logset does not exist                                           |
| 404                       | MachineGroupNotExist | The specified server group does not exist                                           |
| 404                       | ShipperNotExist      | The specified shipping rule does not exist                                         |
| 404                       | TopicNotExist        | The specified log topic does not exist                                         |
| 404                       | ConsumerNotExist     | The specified log topic has no consumption task                                 |
| 405                       | NotSupported         | Unsupported operation                                                 |
| 409                       | IndexConflict        | The same index rule already exists                                         |
| 409                       | LogsetConflict       | The same logset already exists                                           |
| 409                       | MachineGroupConflict | The same server group already exists                                           |
| 409                       | ShipperConflict      | The same shipping rule already exists                                         |
| 409                       | TopicConflict        | The same log topic already exists                                        |
| 409                       | ConsumerConflict     | The consumption task of the log topic already exists                                     |
| 429                       | SpeedQuotaExceed     | Requests are sent too frequently                                                 |
| 500                       | InternalError        | Internal error |

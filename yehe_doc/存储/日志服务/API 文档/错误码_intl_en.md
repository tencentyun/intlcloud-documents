## Feature Description

This document describes the error code and corresponding error message returned when a request fails. You can determine the problem based on the HTTP `StatusCode` and `Body`. The format of `Body` is as follows:

```
{
    "errorcode" : "<ErrorCode>",
    "errormessage" : "<ErrorMessage>"
}
```

## Error Code List

| HTTP  StatusCode | ErrorCode |  ErrorMessage |
| ------------------------- | -------------------- | ------------------------------------------------------------ |
| 400                       | InvalidAuthorization | Invalid signature string format                                             |
| 400                       | InvalidCompressType  | The specified `x-cls-compress-type` is not supported                            |
| 400                       | InvalidContent       | Incorrect message body. Decompressing or parsing failed                             |
| 400                       | InvalidContentType   | The specified `Content-Type` is not supported                                   |
| 400                       | InvalidParam         | Missing or invalid parameter                               |
| 400                       | MissingAgentIp       | Missing `x-cls-agent-ip`                                          |
| 400                       | MissingAgentVersion  | Missing `x-cls-agent-version`                                     |
| 400                       | MissingAuthorization | Missing `Authorization`                                           |
| 400                       | MissingContent       | Empty message body                                                 |
| 400                       | MissingContentType   | Missing `Content-Type`                                            |
| 400                       | TopicClosed          | The collection feature has been disabled for the specified log topic                               |
| 400                       | IndexRuleEmpty       | No index rule has been set for the specified log topic                               |
| 400                       | LogsetNotEmpty       | The specified log topic is not empty and contains log topics                               |
| 400                       | SyntaxError          | Search syntax error                                                 |
| 400                       | LogsetEmpty          | The specified log topic is empty and contains no log topics                         |
| 401                       | Unauthorized         | Authentication failed, probably due to incorrect ID, reused signature, or signature calculation error |
| 403                       | LogsetExceed         | The number of logsets exceeds the upper limit of 20                                 |
| 403                       | LogSizeExceed        | The size of the submitted log exceeds the upper limit of 5 MB                              |
| 403                       | MachineGroupExceed   | The number of server groups exceeds the upper limit of 200                                |
| 403                       | NotAllowed           | This operation is not allowed                                                 |
| 403                       | TopicExceed          | The number of log topics exceeds the upper limit of 10                               |
| 403                       | ShipperExceed        | The number of shipping rules exceeds the upper limit of 10                               |
| 403                       | TaskReadOnly         | Only failed shipping tasks can be restarted. Tasks in other states cannot be modified             |
| 404                       | CursorNotExist       | There are no downloadable logs in the specified location |
| 404                       | TaskNotExist         | The specified shipping task does not exist                                         |
| 404                       | IndexNotExist        | The specified index rule does not exist                                         |
| 404                       | LogsetNotExist       | The specified logset does not exist                                           |
| 404                       | MachineGroupNotExist | The specified server group does not exist                                           |
| 404                       | ShipperNotExist      | The specified shipping rule does not exist                                         |
| 404                       | TopicNotExist        | The specified log topic does not exist                                         |
| 404                       | ConsumerNotExist     | The specified log topic has no consumption tasks                                 |
| 405                       | NotSupported         | Unsupported operation                                                 |
| 409                       | IndexConflict        | The same index rule already exists                                         |
| 409                       | LogsetConflict       | The same logset already exists                                           |
| 409                       | MachineGroupConflict | The same server group already exists                                           |
| 409                       | ShipperConflict      | The same shipping rule already exists                                         |
| 409                       | TopicConflict        | The same log topic already exists                                         |
| 409                       | ConsumerConflict     | The consumption task of the log topic already exists                                     |
| 429                       | SpeedQuotaExceed     | Requests are too frequent                                                 |
| 500                       | InternalError        | Internal error                                                     |

## Description
If an API call fails, the `code` field in the final returned result will not be 0, and a detailed error message will be displayed in the `message` field. You can use `code` and `message` to check the error information in the error code list as shown below:
```
{
   "code": 5100,
   "message": "(100004) The `projectId` is incorrect."
}
```

## Error Codes

### Common errors 

| Error Code | Module Error Code | Error Message                                           | Description                                     | Action                                                     |
| ------ | ---------- | -------------------------------------------------- | ---------------------------------------- | ------------------------------------------------------------ |
| 4000   | 10000      | invalid request parameters                         | The request parameters are invalid.                             | Check the input parameters as described in the documentation.                                     |
| 4000   | 10010      | lacked of required parameters                      | Required parameters are missing.                                 | Enter the required parameters as described in the documentation.                               |
| 4000   | 10110      | request parameters error                           | The parameters are incorrect.                                 | Check whether the parameter values are valid as described in the documentation.                         |
| 4000   | 10280      | action is not existed                              | The requested operation does not exist.                           | Check whether the `action` has been correctly called.             |
| 4000   | 10310      | error: parameter %s key format error               | The format of the `%s` parameter is incorrect.                   | Check the input parameter format as described in the documentation.                 |
| 4000   | 10320      | no such parameter %s                               | The `%s` parameter is missing.                              | Check whether the parameter is valid.                               |
| 4000   | 10330      | parameter %s is NOT a repeatable parameter         | The `%s` parameter cannot be duplicate.                         | Check whether the parameter has been correctly passed.                 |
| 4000   | 10350      | parameter %s value or length is out of range       | The value or length of the `%s` parameter exceeds the specified range.              | Check whether the parameter is valid.                     |
| 4000   | 10360      | parameter %s error type                            | The type of the `%s` parameter is incorrect.                         | Check the parameter as described in the documentation.                 |
| 4000   | 10370      | %s parameter batch size is out of range            | The batch size of the `%s` parameter exceeds the limit.                 | Make sure that the number of input parameters is below the limit.                     |
| 4000   | 10380      | %s parameter is not consequent                     | The `%s` parameter is not consecutive.                       | Make sure that the subscripts are consecutive when passing the parameter in the form of an array.                     |
| 4000   | 10390      | lacked of required parameter %s                    | The `%s` parameter is missing.                              | Enter the required parameter.                             |
| 4000   | 10400      | cannot find parameter %s in uri                    | The `%s` parameter was not found.                            | Enter the required parameter.                             |
| 4000   | 10410      | unexpected http %s only GET or POST is supported   | The `%s` parameter is unexpected, which supports only GET and POST. | Currently, only GET and POST request methods are supported.                             |
| 4000   | 10420      | cannot parse %s, or request size is more than 1MB  | `%s` cannot be processed, or the request size exceeds 1 MB.         | Make sure that the message size is below 1 MB.                      |
| 4000   | 10430      | action name %s is not existed                      | The `%s` operation does not exist.                           | Check the operation.                             |
| 4000   | 10440      | account illegal, it may be an assistant account    | The account is invalid or may be a collaborator account.        | Check whether the account is valid or is a sub-account that has no permissions.   |
| 4000   | 10461      | no cam authentication                              | There is no CAM permission.                            | Check the scope of permissions.                               |
| 4100   | 10030      | authentication failed                              | Authentication failed.                                 | Perform authentication as instructed in [Signature](https://intl.cloud.tencent.com/document/product/213/31575). |
| 4100   | 10080      | secret id status error                             | The `secretId` status is incorrect.                        | Check the validity of the `secretId`.           |
| 4100   | 10270      | secret id is not existed                           | The `secretId` does not exist.                          | Check the validity of the specified `secretId`.           |
| 4300   | 10040      | charge overdue                                     | The account has overdue payments.                               | Top up your account.                         |
| 4420   | 10250      | qps   throttling                                   | The API call rate exceeds the limit.                     | Make sure that the API call rate is below the limit.                       |
| 4480   | 10460      | exceed interface frequency limit, please slow down | The API call rate exceeds the limit.                         | Make sure that the API call rate is below the limit.                       |
| 6000   | 10050      | server internal error                              | An internal error occurred in the service.                             | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |



### Common error codes for queue 

| Error Code | Module Error Code | Error Message                                           | Description                                     | Action                                                     |
| ------ | ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------------- |
| 4000   | 10450         | secret id dosen't begin with AKID                            | The `secretId` does not start with `AKID`.                                    | Check the validity of the `secretId`, which must start with `AKID`. |
| 4000   | 4440 (10100) | queue is not existed, or deleted                             | The queue does not exist or has been deleted.                                   | Check whether the specified queue name is correct.      |
| 4000   | 10692         | delay seconds is out of range                                | The delay exceeds the range.                                             | Check whether the delay range is valid and adjust the delay parameter.                    |
| 6040   | 10660         | it will take some time to release resources of previous queue before you create a new one with the same name, please try later | Failed to create the queue with the same name, because it would take some time to release the resources of the just deleted queue. Currently, to ensure the data consistency, a queue with the same name cannot be created within 30 seconds after a queue is deleted. | Try again later.                                            |
| 6050   | 10670         | your queue cannot be rewinded                                | The queue cannot be rewound.                                                 | The queue cannot be rewound.                                        |


### Common error codes for topic

| Error Code | Module Error Code | Error Message                                           | Description                                     | Action                                                     |
| ------ | ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 4000   | 10490         | number of filterTag exceed limit	filterTag                | The number exceeds the limit of five.                                  | Make sure that the number of filter tags is below the limit.                                       |
| 4000   | 10500         | endpoint format error                                        | The endpoint format is incorrect.                                            | Check the endpoint format for the following errors: (1) The URL contains spaces; (2) The HTTP URL does not start with "http://"; (3) The URL is invalid; (4) The protocol does not correspond to the endpoint. |
| 4000   | 10510         | undefined protocol                                           | The protocol is undefined.                                                 | Check whether the spelling is correct.                                           |
| 4000   | 10540         | there exists subscriptions under this topic, please unsubscribe all of them before DeleteTopic | Make sure that there are no subscriptions to the topic before deleting it to prevent accidental deletion. | Delete all subscriptions first and try again.                                       |
| 4000   | 10590         | (1) topic name format error<br>(2) subscription name format error | (1) The topic name format is incorrect.<br>(2) The subscription name format is incorrect.             | (1) Check whether the topic name format is correct.<br>(2) Check whether the subscription name format is correct.              |
| 4000   | 10630         | illegal endpoint                                             | The endpoint is invalid.                                                | Enter the correct endpoint.                                       |
| 4000   | 10640         | notifyContentFormat of protocol queue must be SIMPLIFIED     | When the value of the `protocol` field is `queue`, the value of `notifyContentFormat` must be `SIMPLIFIED`. | Check the value.                                                   |
| 4000   | 10670         | too many filterTag	filterTag                              | There are too many filter tags.                                     | Check the number of filter tags.                                         |
| 4000   | 10710         | parameters lack of bindingKey                                | `bindingKey` is missing.                                              | Enter `bindingKey`.                                            |
| 4000   | 4440 (10600) | topic is not existed, or   deleted                           | The topic does not exist.                                                   | Check whether the topic is valid.                             |
| 4450   | 10610         | number of topics has reached the limit	Topic              | The number of topics has reached the limit of 1,000.                           | Make sure that the number of topics is below the limit.                                             |
| 4490   | 10470         | subscribtion is already existed                              | A subscription with the same name to the same topic under the same account already exists.                | Select a different subscription.                                           |
| 4500   | 10480         | number of subscription has reached the limit                 | The number of subscriptions to the same topic exceeds the limit of 500.             | Make sure that the number of subscriptions is below the limit.                                             |
| 4510   | 10570         | url connot contain any blank characters                      | The URL cannot contain whitespace characters.                                         | Check whether the URL format is correct.                                               |
| 6040   | 10660         | It will take some time to release resources of previous topic before you can create a new topic with the same name. Please try later. | Failed to create the topic with the same name, because it would take some time to release the resources of the just deleted topic. Currently, to ensure the data consistency, a topic with the same name cannot be created within 30 seconds after a topic is deleted. | Try again later.                                            |



### Module error codes

| Error Code | Module Error Code | Error Message                                           | Description                                     | Action                                                     |
| ------ | ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 4000   | 4460       | queue is already existed,case insensitive                    | The queue already exists.                                                 | Check whether the name is correct.                   |
| 4000   | 10020      | queue name format error                                      | The queue name format is incorrect.                                             | For more information, see the description of the [queueName](https://intl.cloud.tencent.com/document/api/1110/44169) field of the queue creation API. |
| 4000   | 10120      | message body can't be empty                                  | The message content cannot be empty.                                              | Set the message content.                     |
| 4000   | 10470      | receiptHandle error                                          | `receiptHandle` is incorrect.                                         | `receiptHandle` must be a string.                                       |
| 4000   | 10520      | undefined notify retry stragety                              | The message push retry policy is not defined.                                     | Check whether the spelling is correct.                                           |
| 4000   | 10530      | undefined notify content format                              | The message push format is not defined.                                         | Check whether the spelling is correct.                                           |
| 4000   | 10680      | too many bindingKey                                          | The number of `bindingKey` values exceeds the limit.                                          | Make sure that the number of binding keys is below the limit.            |
| 4000   | 10691      | too many delimeters                                          | There are too many delimiters.                                                 | Make sure that the number of delimiters for tags or `bindingKey` values is below the limit. |
| 4000   | 10700      | parameters lack of routingKey                                | `routingKey` is missing.                                              | Add `routingKey`.                                          |
| 4000   | 10720      | too many msgTag                                              | The number of message tags exceeds the limit.                                             | Make sure that the number of tags is below the limit.                 |
| 4100   | 10031      | connection is not authenticated                              | The connection has not been authenticated.                                                 | Authenticate the connection.                                 |
| 4100   | 10032      | connection is already authenticated                          | The connection has already been authenticated.                                                 | Do not authenticate the connection again.                               |
| 4400   | 10230      | exceed maximum message size                                  | The message size exceeds the limit.                                         | Set the message correctly as instructed [here](). |
| 4410   | 10240      | reach maximum retention number of message                    | The number of messages has reached the maximum number of heaped messages.                              | Consume the messages in the queue or increase the maximum number of heaped messages. |
| 4430   | 10260      | receipt handle is invalid                                    | The handler is invalid.                                                     | Check whether the handler is valid.                             |
| 4450   | 10220      | number of queues has reached the limit                       | The number of queues has reached the limit.                                   | [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 4470   | 10300      | total message size exceed 1MB                                | The message size exceeds 1 MB                                              | Adjust the message size.              |
| 4490   | 10770      | message id is invalid                                        | The message ID is invalid.                                                 | Check whether the message ID is valid.             |
| 4490   | 10780      | message operation is not allowed                             | The message status conversion is not allowed.                                         | The transactional message status conflicts with the configured status.                             |
| 4490   | 10790      | transaction message is not supported                         | The queue does not support transactional messages.                                           | The queue does not support transactional messages.                                           |
| 6000   | 10090      | send message failed                                          | Failed to send the message.                                                 | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 6000   | 10130      | recieve message failed                                       | Failed to receive the message.                                                 | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 6000   | 10140      | delete message failed                                        | Failed to delete the message.                                                 | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 6010   | 10150      | delete message partially failed                              | Failed to delete some messages.                                                 | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 6000   | 10160      | get queue attributes failed                                  | Failed to get the queue attributes.                                             | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 6000   | 10170      | set queue attributes failed                                  | Failed to set the queue attributes.                                             | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 6000   | 10180      | delete queue failed                                          | Failed to delete the queue.                                             | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 6000   | 10190      | list queue failed                                            | Failed to get the queue list.                                             | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 6020   | 10290      | batch delete message failed                                  | Batch deletion failed.                                             | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 6030   | 10650      | topic has no subscription, please create a subscription before publishing message | Failed to publish the message, as there are no subscriptions to the current topic.                               | Add a subscription to the current topic.                                       |
| 6030   | 10730      | no bindingKey or filterTag matches the routingKey or msgTag  | The message cannot be delivered, as the message tag cannot match the subscriber's routing key or filter tag. | Check whether the topic subscriber's binding key or the message producer's routing key is correct. |
| 6040   | 10750      | transaction confirmation failed                              | Failed to acknowledge the transactional message.                                             | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 6040   | 10760      | transaction   confirmation partially failed                  | Failed to acknowledge some transactional messages.                                         | An internal error occurred. [Submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for assistance. |
| 6050   | 10740      | too many filterTag or bindingKey                             | The number of filter tags or routing keys exceeds the limit.                           | Make sure that the number of filter tags or routing keys is below the limit.                                             |
| 6070   | 10690      | too many unacked(inactive) messages or delayed messages      | There are too many retained or delayed messages in the current queue.                       | Delete consumed messages.                                 |
| 7000   | 10200      | no message                                                   | There are no messages.                                                     | Make sure that there are messages in the queue before consumption.                   |
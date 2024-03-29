## API Description
This API is used to consume a message in a queue.
Calling the `ReceiveMessage` API will change the status of the obtained message to `inactive`, and the period of being `inactive` is specified by the `visibilityTimeout` queue attribute (for more information, see [CreateCmqQueue](https://intl.cloud.tencent.com/document/api/1110/44169)). We recommend you make the consumer call the `(batch) DeleteMessage` API to delete the message after it successfully consumes the message within the `visibilityTimeout` period; otherwise, the message will return to the `active` status and can be consumed again. This ensures that the message is consumed at least once, but cannot guarantee the idempotency. Therefore, deduplication logic is required on the business side.

The public/private domain names for API requests can be copied from **Queue Service** > **API Request Address** in the [TDMQ for CMQ console](https://console.intl.cloud.tencent.com/tdmq). A sample address is as follows:
- Public network address: `https://cmq-gz.publicXXX.tencenttdmq.com`
- Private network address: `http://gz.mqadapter.cmq.tencentyun.com`


>!
>- The API call URL varies by region.
>- Whenever downstream traffic is generated from using the public domain name, traffic fees will be charged (even during the beta test period). Therefore, we strongly recommend you use the **private** domain name to avoid traffic fees.



## Input Parameters
The list below contains only the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/product/1111/46459).

| Parameter | Required | Type | Description |
|---------|---------|---------|---------|
| queueName | Yes | String | Queue name, which is unique under the same account in an individual region. It is a string of up to 64 characters, which must begin with a letter and can contain letters, digits, and dashes (`-`). |
| pollingWaitSeconds | No | Int | Long polling wait time in seconds. Value range: 0–30. If this parameter is not set, the value of the `pollingWaitSeconds` queue attribute will be used by default. |


## Output Parameters

| Parameter | Type | Description |
|---------|---------|---------|
| code | Int | 0: Success. others: Error. For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/1111/46458). |
| message | String | Error message. |
| requestId | String| Request ID generated by the server, which can be submitted to the backend for troubleshooting when an internal server error occurs. |
| msgBody | String| Body of the consumed message. |
| msgId | String| Unique ID of the consumed message. |
| receiptHandle| String| Unique message handler returned from each consumption, which is used to delete the message. Only a message handler generated from the last consumption can be used to delete the message. After successful consumption within the period of `visibilityTimeout`, you can use the handler to call the `(batch) DeleteMessage` API to delete the message. If `visibilityTimeout` has elapsed, the handler will become invalid. |
| enqueueTime | Int | Time when consumption is created and enters the queue. A Unix timestamp will be returned which is accurate down to the second. |
| nextVisibleTime | Int | Time when a message is visible next time (i.e., consumable again). A Unix timestamp will be returned which is accurate down to the second. |
| dequeueCount | Int | Reserved field. |
| firstDequeueTime | Int | Reserved field. |

## Error Codes
For more information, see [Common Error Codes](https://intl.cloud.tencent.com/document/product/1111/46458).


## Samples

Input:

<pre>
 https://domain/v2/index.php?Action=ReceiveMessage
 &queueName=test-queue-123
 &<<a href="">Common request parameters</a>>
</pre>


Output:

```
{
"code" : 0,
"message" : "",
"requestId":"14534664555",
"msgBody":"helloworld1",
"msgId":"123345346",
"receiptHandle": "283748239349283",
"enqueueTime": 1462351990,
"firstDequeueTime": 1462352990,
"nextVisibleTime": 1462352999,
"dequeueCount": 2
}
```






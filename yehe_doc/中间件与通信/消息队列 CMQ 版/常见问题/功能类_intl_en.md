### Can I use a public domain name for TDMQ for CMQ?
You can use a public domain name for TDMQ for CMQ, which can be obtained in **API Request Address** in the console. However, we recommend you use a private domain name, **as the public domain name incurs fees and may have a higher latency**. 

### Can collaborator accounts use TDMQ for CMQ?
Currently, both collaborators and sub-accounts can use TDMQ for CMQ, but you need to grant them the permissions of TDMQ for CMQ resources in CAM.

### The number of messages in the current queue is less than the number of batch consumed messages in the current request. Will the request be blocked?
No.

### Is the SDK currently in async mode?
All operations of the HTTP SDK are in sync mode, while you can choose async mode in the TCP SDK.

### Can I view the status of queues in the UI?
TDMQ for CMQ provides a visual console, so you can easily view the current queue status.
[Go to the console >>](https://console.intl.cloud.tencent.com/tdmq)

### Does TDMQ for CMQ currently support the MQTT protocol?
No.

### Is there a limit on the size of messages sent and received in TDMQ for CMQ?
Both the message size and request size (for HTTP POST body) in TDMQ for CMQ can be up to 1 MB. **When the message body is larger than 1 KB, we recommend the POST request method, as GET requests will be truncated and trigger exceptions.**
If the message size exceeds 1 MB, you can solve it in the following two ways:
- Store the message in COS, put its object address in TDMQ for CMQ, and download it from COS for processing during consumption.
- Split the message.

### Which access protocols does TDMQ for CMQ use?
TDMQ for CMQ uses HTTP and TCP protocols, and its SDK maintains persistent TCP connections.

### Does TDMQ for CMQ deduplicate messages?
Currently, TDMQ for CMQ does not deduplicate messages. You can refer to [Message Deduplication](https://intl.cloud.tencent.com/document/product/1111/43011) for the cause of duplicate messages and the deduplication scheme.

### How is the long polling in pull mode implemented during message consumption in TDMQ for CMQ?
The queue has the `pollingWaitSeconds` attribute, which indicates the default long polling time for the queue.
If a message is in the queue at the moment of message consumption, the system will return it immediately; otherwise, the system will wait for the time period specified by the `pollingWaitSeconds` parameter. If there is a message during this period, the system will return it. However, if there is still no message after this period, the system will report a no message error.

You can set the `pollingWaitSeconds` attribute of the queue as needed during message consumption instead of using the default value each time a message is consumed.


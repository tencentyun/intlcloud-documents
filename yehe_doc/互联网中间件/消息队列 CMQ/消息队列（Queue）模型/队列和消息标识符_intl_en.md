When using Tencent Cloud CMQ, you need to get familiar with the following three identifiers: queue name, message ID, and receipt handler.

### 1. Queue Name
When creating a queue, you need to provide a unique queue name in the current region. Queue names in different regions can be the same. CMQ uses the region and queue name to uniquely identify a queue. When you want to perform an operation on a queue, you always need to provide these two parameters.

### 2. Message ID

Each message will receive a message ID in the format of `Msg-XXXXXXXX` assigned by the Tencent Cloud system. It is used to identify a message and can be returned to you through the `SendMessage` API request. It should be noted that the message receipt handler instead of message ID is required when a message is deleted.

### 3. Receipt Handler

Whenever a message is received from a queue, a receipt handler of the message will also be received, which is always relevant to the message receipt operation rather than the message itself. To delete a message or modify message attributes, the receipt handler instead of the message ID needs to be provided, which means that a message can be deleted/modified only after it is received.

>If a message is received multiple times, the obtained receipt handler will vary by receipt. When a request to delete a message is initiated, the last received receipt handler needs to be provided; otherwise, the message may not be deleted.

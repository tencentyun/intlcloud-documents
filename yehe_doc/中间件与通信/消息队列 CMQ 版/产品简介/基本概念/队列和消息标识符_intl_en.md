When using TDMQ for CMQ, you need to get familiar with the following three identifiers: queue name, message ID, and receipt handler.

### Queue Name
When creating a queue, you need to give it a unique name in the current region. Queue names can be the same in different regions. TDMQ for CMQ uniquely identifies a queue based on its region and name. When performing an operation on a queue, you always need to provide these two parameters.

### Message ID

Each message will receive a message ID in the format of `Msg-XXXXXXXX` assigned by the Tencent Cloud system. It is used to identify a message and can be returned to you through the `SendMessage` API request. It should be noted that the message receipt handler instead of message ID is required during message deletion.

### Receipt Handler

Whenever a message is received from a queue, a receipt handler of the message will also be received, which is always relevant to the message receipt operation rather than the message itself. To delete a message or modify message attributes, the receipt handler instead of the message ID needs to be provided, which means that a message can be deleted/modified only after it is received.

>?If a message is received more than once, the obtained receipt handler will differ with each receipt. When a message deletion request is initiated, the latest received receipt handler must be provided; otherwise, the message may not be deleted.

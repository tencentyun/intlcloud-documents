### Async Communication Protocol
The message sender can immediately get the returned result after sending a message to CMQ without the need to wait for the recipient's response. The message will be saved in the queue until fetched out by the recipient. The sending and processing of the message are completely async.

### Improved Reliability
In traditional modes, a message request may fail due to long waits; however, if the recipient is unavailable when a message is sent in CMQ, CMQ will retain the message until it is successfully delivered.

### Process Decoupling
CMQ helps reduce the degree of coupling between two processes. As long as the message format stays unchanged, no changes will be made to the sender even if the recipient's API, location, or configuration changes. Moreover, the message sender does not have to know who the recipient is, making the system design clearer; in contrast, if a remote procedure call (RPC) or socket connection is used between processes, when one party's API, IP, or port changes, the other party must modify the request configuration.

### Message Routing
A direct connection is not required between the sender and the recipient, as CMQ guarantees that the message can be routed from the former to the latter. Message routing is even available for two services that are not easily interconnectable.

### Multi-Device Interconnection
Messages can be sent or received among multiple parts in a system, and CMQ controls the availability of messages through message status.

### Diversity
Each queue can be configured independently and not all of them must be identical. Queues in different business scenarios can be customized. For example, if a queue has a longer message processing time, it can be optimized for queue properties.

### SCF Trigger
The CMQ topic model can pass messages to SCF and invoke functions by using the message content and relevant information as parameters.
[SCF product documentation >>](<https://intl.cloud.tencent.com/document/product/583>)

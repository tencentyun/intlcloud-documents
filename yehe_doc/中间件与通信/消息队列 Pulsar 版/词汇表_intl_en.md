### Scheduled Message
After a message is sent to the server, the business may want the consumer to receive it at a later time point rather than immediately. This type of message is called "scheduled message".

### Subscription Type
A subscription type (subscriptionType) is a type of topic subscription by a consumer. You can specify multiple subscription types, such as exclusive, failover, and shared.

### Subscription Name
A subscription name (subscriptionName) uniquely identifies a group of subscribers.

### Partition Index
A partition index (partionindex) denotes the number of a partition in a topic.

### Shared Type
The shared type is a subscription type where a subscriber group can have multiple concurrent active consumer connections, and a message consumed by one of the consumers will not be consumed again by other consumers.

### Namespace
- In TSF, a namespace is an abstract collection of resources and objects. It isolates resources in the same cluster, so you can use the same account to create different environments.
A cluster can have multiple namespaces, but a resource in the cluster can belong to only one namespace. With namespaces, you can divide a cluster into the development environment, test environment, etc. If there are active network connections, services in the same namespace can discover and call each other.
- In TCR, a namespace is a directory hierarchy in an instance like an organization in Docker Hub or a project in Harbor, which can be used to isolate image repositories of different projects, teams, or other organizations. A namespace falls between an instance and a repository, and its access level attribute directly determines the public or private attribute of image repositories in it. Image repositories and Helm chart repositories can share a namespace.
- In TDMQ, a namespace manages associated topics as a group. It is the basic unit of topic management. Each tenant can have multiple namespaces which correspond to different Tencent Cloud environments.

### Exclusive Type
The exclusive type is a subscription type where a subscriber group can have only one active consumer.

### Batch ID
A batch ID (batchid) denotes the number of a message in a batch of messages.

### Producer
A producer refers to a role that sends messages.

### TDMQ
See [TDMQ](https://intl.cloud.tencent.com/document/product/1110/42896).

### Entry
An entry is an element of a ledger, and a ledger is composed of a set of entries.

### Consumer
A consumer refers to a role that receives messages.

### Message ID
A message ID is the unique identifier of a message, which consists of four parts: `ledgerid`, `entryid`, `partionindex`, and `batchid`.
Each message will receive a message ID assigned by the Tencent Cloud system, which can be returned to you through the `SendMessage` API request.

### Message Retention Period
The message retention period refers to the retention period of a message that has been acknowledged by the consumer.

### TDMQ
Tencent Distributed Message Queue (TDMQ) for Pulsar is a proprietary finance-grade distributed message middleware developed based on Pulsar, a top open-source project of Apache. It features high cross-region consistency, reliability, and concurrency. Currently, it is widely used in Tencent's most billing scenarios, including primary payment process as well as real-time reconciliation, monitoring, and big data analysis.

### Message Expiry Time
Message expiry time refers to the time to live (TTL) of an unacknowledged message.

### Topic Type
A topic type is used to identify the type of a topic. Two topic types are supported: persistent and non-persistent. A persistent topic will return an ack for successful delivery after the message is stored to the disk.

### Delayed Message
After a message is sent to the server, the business may want the consumer to receive it after a period of time rather than immediately. This type of message is called "delayed message".

### Failover Type
The failover type is a subscription type where subscribers can exist in a primary/secondary relationship. The primary consumer consumes messages under normal conditions, and consumption will be switched to the secondary consumer when the primary consumer fails.

### Ledger
A ledger is an element in a topic, and a topic is composed of a set of ledgers.

### Topic
- In Oceanus, a topic is the smallest unit of stream connection to subscription and publishing. You can use a topic to denote a type of streaming data, just like a table in a database.
- In IoT Hub, a topic refers to a message communication topic, acting as the communication intermediary of the messages in the Pub/Sub pattern. It is required when publishing and subscribing to messages, and the communication is made based on the specific topic of each device.
- In TDMQ, CKafka, and CMQ, a topic refers to a collection of messages of a particular type. It is a logical concept used to store messages. Topics must be unique in a namespace.
- In CLS, a topic refers to the basic management unit provided by CLS. A log topic corresponds to an application or service and is the smallest management unit in CLS, around which collection, indexing, and delivery are configured. A logset can contain multiple log topics.

### Tenant
A tenant corresponds to an `APPID` in Tencent Cloud.
TDMQ for CMQ currently allows SDK calls based on the TCP protocol for sending and receiving general messages, transaction messages, delayed messages, and async messages. Among them, transaction messages can only be implemented through TCP.
The TCP protocol currently supports public network access and private network access from a CVM instance in a VPC in the same region as the TDMQ for CMQ instance, but does not support the private network access over the classic network.
This document describes how to use the SDK for TCP and install, download, configure, and run the demo to help you quickly build TDMQ for CMQ test projects.

## TCP Protocol Advantages
- **Fewer computing resources**
HTTP authenticates requests and requires a signature for each request, while TCP authenticates links; therefore, it is sufficient to authenticate a link during its establishment, which saves client computing resources.
- **Safer client threads**
The TCP client is thread-safe, and multiple threads can use the same link, which saves link resources.
- **Higher transfer efficiency**
TCP increases the proportion of valid data during transfer. For the same client, it has higher throughput and QPS and greater transfer efficiency than HTTP.
- **Better user experience**
TCP supports async APIs and callbacks.
- **More features**
TCP supports the latest TDMQ for CMQ feature of distributed message transaction.

## Demo Usage
### Preparing demo environment
1. **Install IDEA**
You can install IntelliJ IDEA or Eclipse. This document uses IntelliJ IDEA as an example.
[Download IntelliJ IDEA Ultimate](https://www.jetbrains.com/idea/) and install it accordingly.
2. **Download the demo**
[Download the TDMQ for CMQ demo](https://github.com/tencentyun/cmq-java-tcp-sdk) to your local system and decompress it. You will see the `cmq-java-tcp-sdk-master` folder then.

### Configuring demo
1. **Create a resource**
You need to create the required TDMQ for CMQ resource in the console and get the TDMQ for CMQ queue name, `SecretID`, and `SecretKey`.
For detailed directions, see [Queue Model](https://intl.cloud.tencent.com/document/product/1111/42991).
2. **Import demo files**
Open the folder on the startup page of IDEA.
![](https://main.qcloudimg.com/raw/8a3ba96ef290ad50f6f0d20c01594f5d.png)
After the folder is opened, the file hierarchy is as follows, and the demo files are stored in the `demo` folder.
![](https://main.qcloudimg.com/raw/1fc9235f7ae621fec4105fb173725d89.png)
3. **Configure demo parameters**[](id:demo)
Modify the file NameServer address, key pair, and queue name.
Taking ProducerDemo as an example, the configuration is as follows:
```java
producer.setNameServerAddress("Corresponding NameServer");
producer.setSecretID("Obtained SecretID")
producer.setSecretKey("Obtained SecretKey")
String queue = "Name of the created queue"
```
The details are as follows:
![](https://main.qcloudimg.com/raw/f4a7604ccb2319befdcbe338f40be939.png)

### Running demo
#### Sending and receiving message with queue model
 1. [Configure demo parameters](#demo).

 2. After the `ProducerDemo` file is successfully executed, the log will be displayed as follows:
 ![](https://main.qcloudimg.com/raw/dfb74dac5c9dc5550697f9f9628f1259.png)
    ProducerDemo supports sending general messages, delayed messages, and async messages.

 3. Execute the `ConsumerDemo` file to receive messages.


#### Sending and receiving message with topic model
 1. Run the `PublishDemo` class to send messages with the topic model.
 2. Run the `SubscriberDemo` class to receive messages with the topic model.

#### Sending and receiving transaction messages
 1. Run the `ProducerTransactionDemo` class to send transaction messages.
 2. Run the `SubscriberTransactionDemo` class to receive transaction messages.


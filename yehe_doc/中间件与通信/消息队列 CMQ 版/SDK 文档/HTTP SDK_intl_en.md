## Overview
TDMQ for CMQ currently supports SDKs for Java, Python, PHP, and C++ and will support SDKs for more languages in the future. Developers are welcome to develop SDKs for more languages according to the API descriptions.
As it takes about 1 second to assign and release resources, the TDMQ for CMQ SDK will have a delay of 1 second when creating and deleting queues and topics, and we recommend you add the creation and deletion time intervals in your program so as to ensure successful calls.

## Download Address

The GitHub addresses of SDKs for different languages are as follows:
- [SDK for Java](https://github.com/tencentyun/cmq-java-sdk)
- [SDK for Python](https://github.com/tencentyun/cmq-python-sdk) (the default SDK is for Python 2, and you can switch to the Python 3 branch to view the SDK for Python 3)
- [SDK for PHP](https://github.com/tencentyun/cmq-php-sdk)
- [SDK for C++](https://github.com/tencentyun/cmq-cpp-sdk)

## Notes
Before using the SDK, you must get at least the [SecretId](https://console.cloud.tencent.com/capi), [SecretKey](https://console.cloud.tencent.com/capi), and API access address (i.e., to which region requests are sent over the private network or public network). The API access address is as described below:

#### Queue model
**Replace `{$region}` in the domain name with the corresponding region:**

- AIP public domain name: `https://cmq-{$region}.public.tencenttdmq.com`
- API private domain name: `http://{$region}.mqadapter.cmq.tencentyun.com`


#### Topic model[](id:topic)
**Replace `{$region}` in the domain name with the corresponding region:**
- AIP public domain name: `https://cmq-{$region}.public.tencenttdmq.com`
- API private domain name: `http://{$region}.mqadapter.cmq.tencentyun.com`

If your business process is also deployed on a CVM instance, we strongly recommend you use the private network access in the same region; for example, for a CVM instance in the Beijing region, we recommend you use `http://bj.mqadapter.cmq.tencentyun.com` for the following reasons:
- The private network in the same region has a lower latency.
- Currently, TDMQ for CMQ charges traffic fees for public network downstream traffic, which can be saved if you use the private network.

#### Description
`{$region}` needs to be replaced with a specific region: gz (Guangzhou), sh (Shanghai), bj (Beijing), hk (Hong Kong (China)), or cd (Chengdu). The value of `region` in the common parameters should be the same as that of `region` in the domain name; otherwise, the latter will prevail, i.e., requests will be sent to the region as specified by `region` in the domain name.


## Demo Usage
### Preparing demo environment
1. **Install IDEA**
You can install IntelliJ IDEA or Eclipse. This document uses IntelliJ IDEA as an example.
[Download IntelliJ IDEA Ultimate](https://www.jetbrains.com/idea/) and install it accordingly.
2. **Download the demo**
[Download the TDMQ for CMQ HTTP demo](https://github.com/tencentyun/cmq-java-sdk) to your local system and decompress it. You will see the `cmq-java-sdk-master` folder.


### Configuring demo
1. **Create a resource**
You need to create the required TDMQ for CMQ resource in the console and get the TDMQ for CMQ queue name, `SecretID`, and `SecretKey`.
For detailed directions, see [Queue Model](https://intl.cloud.tencent.com/document/product/1111/42991).
2. **Import demo files**
Open the folder on the startup page of IDEA.
![](https://main.qcloudimg.com/raw/8a3ba96ef290ad50f6f0d20c01594f5d.png)
After the folder is opened, the demo files are stored in the `/src/main/java/com/qcloud/cmq/example` folder.
3. **Configure demo parameters**
Modify the file request address, key pair, etc. Taking `Producer` as an example, the configuration is as follows:
```java
String secretId="Obtained SecretID";
String secretKey="Obtained SecretKey";
String endpoint = "https://****.com";
String queueName = "test";
```
Select **Create Queue** or **Use Existing Queue**:
```java
// Create a queue and set its attributes
QueueMeta meta = new QueueMeta();
meta.pollingWaitSeconds = 10;
meta.visibilityTimeout = 10;
meta.maxMsgSize = 1048576;
meta.msgRetentionSeconds = 345600;
Queue queue = account.createQueue(queueName,meta);
```
```java
// Use an existing queue in the console
Queue queue = account.getQueue(queueName);
```
This demo uses an existing queue of the current account. To select **Create Queue**, replace the value of `queueName` with the name of the queue to be created, and then uncomment the code for queue creation.
Commenting code is a common operation. Use the "deletion" operation with caution. You can configure other classes as configured in the `Producer` class.

### Running demo
#### Sending and receiving message with queue model
Run the `Producer` class to send a message first and then run the `Consumer` class to receive the message.  
Sample code for sending message:
```java
String msg = "hello!";
String msgId = queue.sendMessage(msg);
System.out.println("==> send success! msg_id:" + msgId);
```
Sample code for receiving message:
```java
Message msg = queue.receiveMessage(10);
```
#### Sending and receiving message with topic model
Run the `TopicDemo` class. For the topic model request domain name, see [Topic Model Request Domain Name](#topic).  
Sample code for publishing message:

```java
String msg = "hello!";
String msgId = topic.publishMessage(msg);
```
Sample code for processing message:
```java
String queueName = "test";
String subscriptionName = "sub-test";
String Endpoint = queueName;
String Protocol = "queue";
account.createSubscribe(topicName,subscriptionName, Endpoint, Protocol);
```
Enter a queue name to process messages when creating a subscriber.

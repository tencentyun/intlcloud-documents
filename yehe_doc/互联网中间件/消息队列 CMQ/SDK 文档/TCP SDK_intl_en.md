CMQ currently allows SDK calls based on the TCP protocol for sending and receiving general messages, transaction messages, delayed messages, and async messages. Among them, transaction messages can only be implemented through TCP.
The TCP protocol currently supports public network access and private network access from a CVM instance in a VPC in the same region as the CMQ instance, but does not support the private network access over the classic network.
This document describes how to use the SDK for TCP and install, download, configure, and run the demo to help you quickly build CMQ test projects.
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
TCP supports the latest CMQ feature of distributed message transaction.

## Demo Usage
### Preparing demo environment
1. **Install IDE**
You can install IntelliJ IDEA or Eclipse. This document uses IntelliJ IDEA as an example.
Please [download IntelliJ IDEA Ultimate](https://www.jetbrains.com/idea/) and install it accordingly.
2. **Download the demo**
Please [download the CMQ demo ](https://github.com/tencentyun/cmq-java-tcp-sdk) to your local system and decompress it. You will see the `cmq-java-tcp-sdk-master` folder then.

### Configuring demo
1. **Create a resource**
You need to create the required CMQ resource in the console and get the CMQ queue name, `SecretID`, and `SecretKey`.
For detailed directions, please see [Queue Model](https://intl.cloud.tencent.com/document/product/406/8436) and [Topic Model](https://intl.cloud.tencent.com/document/product/406/8437).
2. **Import demo files**
Open the folder on the startup page of IDEA.
![](https://main.qcloudimg.com/raw/8a3ba96ef290ad50f6f0d20c01594f5d.png)
After the folder is opened, the file hierarchy is as follows, and the demo files are stored in the `demo` folder.
![](https://main.qcloudimg.com/raw/1fc9235f7ae621fec4105fb173725d89.png)
3. **Configure demo parameters**<span id="peizhi"></span>
Modify the file NameServer address, key pair, and queue name. For the NameServer address, please see the [NameServer Table](#Nameserver).
Taking ProducerDemo as an example, the configuration is as follows:
```
producer.setNameServerAddress("Corresponding NameServer");
producer.setSecretID("Obtained SecretID")
producer.setSecretKey("Obtained SecretKey")
String queue = "Name of the created queue"
```
The details are as follows:
![](https://main.qcloudimg.com/raw/63f196eb05b263cff7f4ea5c8881a8c1.png)

### Running demo
#### Sending and receiving messages with queue model
 1. [Configure demo parameters](#peizhi).
 2. After the `ProducerDemo` file is successfully executed, the log will be displayed as follows:
 ![](https://main.qcloudimg.com/raw/151a28f513b8eebe78eea9e47fe2b732.png)
 ProducerDemo supports sending general messages, delayed messages, and async messages.
![](https://main.qcloudimg.com/raw/0562f412da247090198fb79540d90d8e.png)
 3. Execute the `ConsumerDemo` file to receive messages.

#### Sending and receiving messages with topic model
 1. Run the `PublishDemo` class to send messages with the topic model.
 2. Run the `SubscriberDemo` class to receive messages with the topic model.

#### Sending and receiving transaction messages
 1. Run the `ProducerTransactionDemo` class to send transaction messages.
 2. Run the `SubscriberTransactionDemo` class to receive transaction messages.

## NameServer Table<span id="Nameserver"></span>
| Region     | Public Network Address   | VPC Address       |    
| -------- | ------------ | -------------------------- | 
| India     | http://cmq-nameserver-in.tencentcloudapi.com | http://cmq-nameserver-vpc-in.api.tencentyun.com | 
| Beijing     | http://cmq-nameserver-bj.tencentcloudapi.com| http://cmq-nameserver-vpc-bj.api.tencentyun.com |   
| Shanghai     |http://cmq-nameserver-sh.tencentcloudapi.com| http://cmq-nameserver-vpc-sh.api.tencentyun.com |  
| Guangzhou     | http://cmq-nameserver-gz.tencentcloudapi.com | http://cmq-nameserver-vpc-gz.api.tencentyun.com |  
| North America     | http://cmq-nameserver-ca.tencentcloudapi.com| http://cmq-nameserver-vpc-ca.api.tencentyun.com |   
| Chengdu     | http://cmq-nameserver-cd.tencentcloudapi.com | http://cmq-nameserver-vpc-cd.api.tencentyun.com|    
| Chongqing     | http://cmq-nameserver-cq.tencentcloudapi.com | http://cmq-nameserver-vpc-cq.api.tencentyun.com |    
| Hong Kong (China)     |http://cmq-nameserver-hk.tencentcloudapi.com | http://cmq-nameserver-vpc-hk.api.tencentyun.com |    
| Korea     | http://cmq-nameserver-kr.tencentcloudapi.com | http://cmq-nameserver-vpc-kr.api.tencentyun.com |     
| Russia   | http://cmq-nameserver-ru.tencentcloudapi.com | http://cmq-nameserver-vpc-ru.api.tencentyun.com|     
| Singapore   | http://cmq-nameserver-sg.tencentcloudapi.com                 | http://cmq-nameserver-vpc-sg.api.tencentyun.com          |          
| Thailand     | http://cmq-nameserver-th.tencentcloudapi.com| http://cmq-nameserver-vpc-th.api.tencentyun.com |     
| East US     | http://cmq-nameserver-use.tencentcloudapi.com | http://cmq-nameserver-vpc-use.api.tencentyun.com        |  
| West US     | http://cmq-nameserver-usw.tencentcloudapi.com | http://cmq-nameserver-vpc-usw.api.tencentyun.com |     


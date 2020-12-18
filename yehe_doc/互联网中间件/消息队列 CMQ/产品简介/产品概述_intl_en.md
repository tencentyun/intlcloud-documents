## CMQ Overview
Cloud Message Queue (CMQ) is a distributed message queue system based on Tencent's proprietary message engine. It ensures strong message consistency by leveraging Tencent's proprietary distributed Raft algorithm and offers high message reliability by storing three synchronous copies of messages. Specifically, with its advantages of high reliability, availability, performance, and scalability, it provides a rich set of services such as message queue, publish/subscribe model, message rewind, delayed message sending, sequential message sending, and message track. Over its development and iteration in more than seven years, CMQ asynchronously serves Tencent's major businesses such as WeChat, WeBank, QQ Show, and Mobile QQ.

CMQ has been put into formal commercial use and provides a highly available cloud message service in multiple Tencent Cloud regions around the globe. Its data center hardware is constructed in compliance with the high standards of Tencent Cloud IDCs. In a single region, CMQ is deployed across multiple data centers, so that it can still provide message services for applications even if a data center becomes entirely unavailable. In addition, it is also deployed in the Shenzhen and Shanghai Finance Zones to provide finance-grade high-reliability message queue services.

Currently, CMQ supports connection over HTTP, HTTPS, and TCP and can be integrated through SDKs for various programming languages such as PHP, Java, and Python.


| Connection Method | HTTP/HTTPS Connection | TCP Connection |
| :-------- | :--------| :------ |
| **Application scenarios** | It provides sync HTTP/HTTPS-based connection and can be simply and easily integrated through RESTful APIs and SDKs for multiple programming languages. | It supports sync/async TCP-based connection and SDKs for multiple programming languages, which improves the producer and consumer efficiency and increases the performance of the message queue service. |
| **Strengths**    | It features unlimited message retention, finance-grade horizontal scalability and high reliability, and messages can be stored in disks in real time. | It features unlimited message retention, finance-grade horizontal scalability and high reliability, and messages can be stored in disks in real time. In addition, messages can be received and sent in an async non-blocking TCP method, which improves the efficiency. |

>?
>- TCP-based connection to CMQ is currently in beta test. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=947&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CMQ&step=1) for application.
>- CMQ supports deployment in private cloud. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=947&source=0&data_title=%E6%B6%88%E6%81%AF%E9%98%9F%E5%88%97%20CMQ&step=1) for application.


## Use Case Overview


CMQ is recommended in scenarios where async communication is required; for example:

- Your application requires guaranteed message transfer reliability. When a message is sent, even if the recipient is unavailable due to problems such as power failure, server downtime, and CPU overload, the recipient can still receive it once becoming available. Traditional message queues store messages in the memory and therefore cannot achieve this effect. In the distributed message queues of CMQ, messages will be persistently stored until the recipient successfully gets them.

- Your business needs to run properly as the access traffic and number of messages retained in the queue soar. In traditional message queues, messages are stored in the local memory, and since the processing capabilities and memory capacity of a single server are limited, scalability is unavailable. In contrast, the distributed architecture of CMQ guarantees easy scalability, and more importantly, scaling is completely imperceptible to users.

- Two services need to communicate with each other when their networks cannot interconnect or the application route information (such as IP and port) is variable. For example, if two Tencent Cloud services want communication without knowing each other's address, they can agree on the queue name so that one service can send messages to the queue and the other can receive messages from it.

- The communication between system components or applications is frequent, they need to maintain the network connections to each other, and there are multiple types of communicated content. In this case, the system design will be very complicated if a traditional architecture is used. For example, when a central processing service needs to assign tasks to multiple task processing services (similar to the master/worker mode), the master needs to maintain connections with all workers and detect whether the workers start processing the tasks so as to determine whether task reassignment is required. At the same time, workers need to report the task results to the master. Maintaining such a system will result in complicated design and high implementation difficulty and costs. As shown below, the system can be made much simpler and more efficient when CMQ is used to reduce the coupling between the master and workers.
![](https://main.qcloudimg.com/raw/cc131faa0a65e708136df813cfe1e581.png)

- The coupling between system components or applications is tight, and you want to reduce the coupling degree especially when your control over the dependent components is weak. For example, the CGI of your business receives contents submitted by users, stores some data in its own system, and forwards the processed data to other business applications (such as data analysis and storage systems). In traditional solutions, services connect to each other through sockets, and if the IP or port of the recipient changes or the recipient is replaced, the data sender needs to modify the relevant information accordingly. In contrast, if CMQ is used, the recipient and sender are imperceptible to each other's information, which greatly reduces the coupling degree.

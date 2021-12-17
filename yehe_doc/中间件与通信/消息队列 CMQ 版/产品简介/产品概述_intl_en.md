TDMQ for CMQ is a distributed message queue service that features a reliable message-based async communication mechanism. It enables message sending/receiving among different applications deployed in a distributed manner (or different components of the same application) and stores the delivered messages in reliable and valid message queues to prevent message loss. It supports multi-process simultaneous read/write, so that message sending and receiving do not interfere with each other, eliminating the need for the applications or components to keep running.

TDMQ for CMQ supports queue and topic patterns and is suitable for various scenarios, such as async notification, remote call, and topic message delivery. It is widely used in actual businesses, including order processing, time-consuming event callback, and operations system logging. Moreover, it can retain millions of messages to guarantee that messages will not get lost.

TDMQ for CMQ currently supports connection over HTTP and TCP.


| Connection Method | HTTP Connection | TCP Connection |
| :----------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **Application scenarios** | It provides sync HTTP-based connection and can be simply and easily integrated through RESTful APIs and SDKs for multiple programming languages. | It supports sync/async TCP-based connection and SDKs for multiple programming languages, which improve the producer and consumer efficiency and increase the performance of the message queue service. |
| **Strengths**    | It features unlimited message retention, finance-grade horizontal scalability, and high reliability, and messages can be stored in disks in real time. | It features unlimited message retention, finance-grade horizontal scalability, and high reliability, and messages can be stored in disks in real time. In addition, messages can be received and sent in an async non-blocking way over TCP, which improves the efficiency. |


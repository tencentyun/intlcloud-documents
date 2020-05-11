Serverless Cloud Function (SCF) is constantly developing and upgrading. It can be used in more use cases thanks to its growing capability and better compatibility with other products.

## Mobile and Web Applications

SCF can serve as a backend for mobile and web applications to implement the server-side application logic and provide services through APIs. By integrating it with Cloud Memcached, COS, TencentDB, and other Tencent Cloud products, you can build elastically scalable mobile and web applications and create rich-featured serverless backends with ease, which can run in multiple IDCs with high availability and eliminate your needs to manage scalability and backup redundancy.

## File Processing and Notification

By using COS as a function trigger, event notifications can be sent when a file in a COS bucket changes, which enables prompt processing of the changed file and business notification.

For example, when an image is uploaded to a COS bucket, a function can be notified immediately, and the image can be immediately obtained for corresponding operations such as cropping, thumbnailing, and watermarking, realizing automatic image processing. Plus, the image can be written to a database for future use after processed.

## Message Relay

CMQ and CKafka can be used as function triggers, so that when a message is received, a function can be triggered, and the message will be passed to the function as event content.

For example, when a log of a business system is received in CKafka, the function can write the log content as a file to COS for log archival and storage.

## Business Flow

As the intermediate channel of business event flow, CMQ can be connected to multiple functions to realize business state flow and assignment. The business logic judgment and processing in the functions can perform different channel assignment, state flow, and event distribution according to the contents of the business messages, helping connect complex business processes.



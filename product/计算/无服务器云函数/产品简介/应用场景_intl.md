Serverless Cloud Function (SCF) is constantly developing and upgrading. SCF can be used in more use cases due to its growing capability and better compatibility with other products.


## API Service

Used in conjunction with API Gateway, SCF can serve as a backend for mobile apps and web applications to implement the server-side application logic and provide services through APIs.

Just like a traditional API service backend, SCF can implement business logic and achieve storage of the backend data in the API service by connecting with Cloud Memcached, COS, and TencentDB.

## File Processing and Notification

By using COS as a function trigger, event notifications can be sent when a file in a COS bucket changes, which enables prompt processing of the changed file and business notification.

For example, when an image is uploaded to a COS bucket, an function can be notified immediately, and the image can be immediately obtained for corresponding operations such as cropping, thumbnailing, and watermarking, realizing automatic image processing. Plus, the image can be written to a database for future use after processed.

## Message Relay

CMQ and CKafka can be used as function triggers, and when a message is received, an function can be triggered and the message is passed to the function as event content.

For example, when a log of a business system is received in CKafka, the function can write the log content as a file to COS for log archival and storage.

## Business Flow

As the intermediate channel of business event flow, CMQ can be connected to multiple functions to realize business state flow and assignment. The business logic judgment and processing in the functions can perform different channel assignment, state flow, and event distribution according to the contents of the business messages, helping connect complex business processes.

## AI Reasoning

By using a trained AI model in a function and providing an API service through API Gateway, AI reasoning can be initiated only when a request arrives. This reduces server costs by eliminating the need to prepare servers or GPU servers, allows billing by actual calls, and enables automatic elastic scaling in case of high volumes of concurrent requests.

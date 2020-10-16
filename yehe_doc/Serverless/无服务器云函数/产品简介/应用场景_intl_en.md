Serverless Cloud Function (SCF) is constantly being developed and upgraded. With increasing capabilities and compatibility with other products, SCF can be used in more use cases.

## File Processing and Notifications

By using COS as a function trigger, event notifications can be sent when a file in a COS bucket changes, which enables the prompt processing of the changed file and business notifications.

For example, once an image is uploaded to a COS bucket, the cloud function is notified immediately, and the image can be immediately obtained for automatic processing, such as cropping, thumbnailing, and watermarking. In addition, the processed image can be written to a database for future use.


## Data ETL Processing

Some data processing systems need to process huge amounts of data frequently, either periodically or planned.

For example, a securities company needs to collect statistics on its transactions every 12 hours and determine the top 5 transaction volumes. Another example is that a flash sale website needs to process its transaction flow logs once a day to obtain errors caused by the resources being sold out and thereby analyze the website buzz and trends. Possessing great scalability, SCF facilitates the computation of large-volume data. SCF also enables the concurrent execution of multiple mapper and reducer functions on the source data, and finishes the tasks in a short period of time. Compared with traditional functions, SCF reduces costs by preventing resources from being idleness and wasting resources.



## Mobile and Web Applications

Cloud functions let you run mobile and web application backend code to implement the server-side application logic and provide services through APIs. By using SCF with Cloud Cache, TencentDB, COS, and other products, developers can build mobile and web applications with elastic scalability and create various serverless backends. These applications can run in multiple IDCs with high availability. You don’t need to manage the scalability and backup redundancy.


## AI Inference

After an AI model is trained and ready to provide inference services, you can use SCF to encapsulate the model into a function. The code is executed upon request reception. In this way, you only need to pay on demand without investing in servers and GPUs to get the automatic scaling capability featuring high request concurrency.

## Message Relay

CMQ and CKafka can be used as function triggers. A received message triggers the execution of the cloud function, and the message is passed to the cloud function as the event content.

For example, when CKafka receives a log of a business system, the cloud function can write the log content as a file to COS for log archive and storage.

## Business Flow

As the intermediate channel of business event flow, CMQ connects multiple functions for business status flow and assignment. According to the messages, business logic judgment and processing in the functions can be performed to implement channel assignment, status flow, and event distribution, which connect the complex business processes.



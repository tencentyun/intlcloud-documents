## Customer Overview

Tencent Games under Interactive Entertainment Group (IEG) focuses on game development and operations and maintains major online game communities. On its journey to cloud gaming, IEG has been constantly driving and making breakthroughs. In March 2021, IEG launched an online game development platform called "Proxima Game Online Service" (PGOS) as part of its global business, which provides:

- **Backend service platform:** PGOS is an online game solution designed to facilitate game backend development and maintenance and reduce costs, so that developers can focus on the development of gameplay and core logic.
- **Fully managed service:** its complete backend solution eliminates the challenges in setting up, managing, and running servers at scale. Its automatically scalable dedicated servers provide a low latency and high reliability for real-time gaming.
- **One-Stop control panel:** developers and OPS personnel can retrieve player information, view logs, monitor real-time data, and edit service configurations on the its web portal.
- **Cross-platform SDK:** it provides out-of-the-box SDKs for C++ and UE4, making it easy for developers to use the PGOS service on game clients and internal servers.
- **Flexible matching rules:** it enables players to accurately and quickly match up with other players in real-time battles.
- **Scalability and flexibility:** its entire system uses a microservice architecture rather than integrated hierarchical architecture, allowing developers to add and modify interactions between corresponding services.




## Serverless Solution

Tencent Cloud Serverless naturally supports the above features provided by PGOS and is used by it to provide underlying computing support, better helping teams migrate to the cloud quickly.

- **Out-of-the-Box serivce:** Tencent Cloud Serverless enables you to focus entirely on business code with no need to purchase, set up, and configure servers. Its architecture not only helps accelerate game publishing and iteration but also significantly reduces the OPS costs. In addition, it guarantees the stability and security of your business and the availability of the resources, eliminating your concerns over underlying resources.
- **Dynamic scaling:** another benefit of serverless is auto scaling, which makes it easier for your business to withstand traffic surges. Auto scaling guarantees normal business operations when access traffic surges and reduces costs during off-peak hours.
- **Real-Time monitoring:** Tencent Cloud Serverless offers real-time logs and a monitoring dashboard, where R&D and management personnel can monitor business operations in real time. In addition, it is connected to Cloud Monitor to provide alarming capabilities in multiple dimensions such as execution duration and status exception. In this way, you can discover problems and get notified as soon as they occur.
- **Scalability and flexiblity:** the atomic feature of FaaS naturally supports flexible business expansion. Different SCF functions can support independent features, such as mutual function invocation, separate update and deployment, and online function code editing. Tencent Cloud Serverless offers a one-stop solution from business development, deployment, to monitoring.
- **Multiple event triggering methods:** Tencent Cloud Serverless supports around 10 event triggering methods, including timer trigger, API Gateway trigger, and COS trigger, meeting your diverse needs in different scenarios.



#### How serverless supports cloud gaming with computing power

Tencent Cloud Serverless can provide underlying computing support for the global business of PGOS. You can create one virtual server (corresponding to one or more SCF functions) and write relevant business logic. PGOS relies on it to offer complete monitoring and logging capabilities and connect to backend services. It further encapsulates DevOps tools and furnish fully managed and automatically built and deployed features.

<img src="https://main.qcloudimg.com/raw/8e45feb831d948d09ec66fb835d48715.png"/>

PGOS provides multiple drive methods, and the underlying layer triggers business operations on the virtual server with different function triggers.

- **Timer drive**: a scheduled task can be configured for a game on the web portal to trigger a specific API of the virtual server.
- **Event drive**: the virtual server can listen on specific events and will be automatically triggered when events occurs.
- **Game drive*: the game client or DS can actively invoke extension interfaces and trigger specific APIs of the virtual server through the gateway.
- **Manual drive:** you can manually run/trigger the specific APIs of the virtual server in the web portal.

<img src="https://main.qcloudimg.com/raw/bc4147b4356532827e9121320dc09a14.jpeg"/>


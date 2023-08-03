


## Overview
As a new type of cloud integration service, Tencent Integration Platform(iPaaS) fully utilizes elastic scaling, container, resource management, and self-service capabilities to connect different systems and applications in and outside your organization to the same platform through little to no code. With best integration practices and the ability to quickly build system integration models, it offers various features, including resource integration, data orchestration, and business connection between systems, making it a lightweight, comprehensive, and flexible integration system. It also provides rich application management and Ops capabilities as well as visual monitoring and log pages to further reduce your operational costs. iPaaS offers a full range of integration capabilities that combine development, debugging, publishing, and Ops, greatly improving your integration efficiency and reducing the late Ops costs of integration tasks.

<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/mjCu132_%E4%BA%A7%E5%93%81%E6%A6%82%E8%BF%B0.jpg" width="400px">



As enterprises' internal and external systems have complicated network topologies and highly sensitive data and are managed in multiple or hybrid clouds, iPaaS provides two solutions: in-cloud and off-cloud business system connection through a security gateway and on-premises platform deployment. It breaks through the barriers of different regions and architectures so that data can flow throughout the entire domain, while guaranteeing the security of business data and the reliability of integrations.
![3](https://document-1259649581.cos.ap-guangzhou.myqcloud.com/eis/3.png)



## Features

### Communication protocol connector

iPaaS offers mainstream communication protocol connectors such as FTP, HTTP, Advanced Message Queuing Protocol (AMQP), and Applicability Statement (AS) 1/2/3/4 connectors. 


### SaaS application connector

As SaaS applications gain popularity, connectivity of out-of-the-box applications is becoming increasingly important. Through the SaaS application connector, you can simply connect different services together. iPaaS has published connectors for over 200 applications, including WeCom, Tencent Meeting, Tencent QiDian, and Tencent Lexiang. In addition, it also opens up an application connector ecosystem to empower more SaaS vendors to publish their own application connector components based on the SDK.

### Data mapping and transformation

As the core features of iPaaS, data transformation and orchestration eliminate the technological differences between heterogeneous applications, making different application services communicate and collaborate with each other smoothly.
After connecting your data to iPaaS, you can orchestrate and convert the formats and structures of the input data to those of the target system; for example:

- Data format conversion: XML to JSON.
- Data mapping: Data structure conversion and field mapping.
- Content modification: Parameter modification and variable assignment.


### Message routing

In many scenarios, such as data splitting, aggregation, sorting, and distribution, the message direction in a flow needs to be controlled. iPaaS provides diverse components for controlling the flow of messages. For example, the Choice component can act like if-else branch logic in program design to first match and judge the first if condition. If the preorder condition is hit, the component will process the nodes under the condition; otherwise, it will continue matching the subsequent if conditions.

### Versioning
iPaaS allows you to publish different versions of your integration apps to cope with dynamic requirements such as business changes and version upgrades.

### Integration app log
iPaaS offers real-time and historical logs of your integration apps to help you with security analysis, compliance auditing, resource tracking, and problem locating.

### Secure transfer
iPaaS offers multiple data security mechanisms, including data security (sensitive data encryption), system security, network security (firewall), and business security (tenant isolation).

### Development capabilities 
Dataway is an expressive script language for custom data conversion and processing in iPaaS. It is integrated in the iPaaS runtime service and plays a key role in implementing iPaaS extensibility.
iPaaS's many built-in components can provide Dataway script-based customization capabilities to dynamically process connector events.

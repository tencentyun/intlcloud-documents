 
Dataway
As the expression evaluator of iPaaS, Dataway can flexibly control message data through operations such as filtering, mapping, and format conversion. To build a general platform, each component must have a certain level of dynamic value calculation capabilities to handle different scenarios, and Dataway is the key tool to implement such capabilities.

 
iPaaS
Integration Platform as a Service (iPaaS) is generally used for cloud service, application, data, and B2B ecosystem integration and has been gaining popularity in extended scenarios, including API publishing, mobile application integration, and IoT.

 
Integration flow
An integration flow is the process for completing a specific integration business scenario; for example, you can build the process of syncing the master data of an organizational structure from ERP to the HR system as an independent flow. In a flow, you can define data flows between multiple business systems through visual configuration to implement real-time or quasi-real-time service orchestration capabilities, so as to integrate data between two or more systems.

Integration app
An integration app represents a complete business integration project, such as integration of Salesforce and SAP ERP, involving things like customer data sync, sales order sync, service order sync, and conversion of sales leads to orders. An integration app can consist of multiple integration flows.

 
Message
In TDMQ for CMQ, a message refers to the content delivered between different processes, which contains data and attributes.
In iPaaS, a message refers to the data structure passed between each connector instance and processor instance in an integration flow.
 
Component
A component is a data processing unit that can process the input data and output the processing result according to the specified logic. You can implement it by customizing code as needed or by using the platform's preconfigured general processing logic.
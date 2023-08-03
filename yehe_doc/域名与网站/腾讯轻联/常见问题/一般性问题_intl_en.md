### What is iPaaS?

As a new type of cloud integration service, iPaaS natively features elastic scalability, high availability, and self-service. It connects different systems in and outside your organization to the same platform.

### What integration scenarios is iPaaS suitable for?

With high availability and complete technical support, iPaaS is suitable for many enterprise-level integration scenarios, including integrating applications, data, B2B ecosystem, and IoT systems. 

### How do I get started with iPaaS?

After connecting to the iPaaS console, you can start creating, deploying, running, managing, and monitoring integration apps to interconnect your systems.

### How does iPaaS integrate the data of complex business logic?

The integration platform of iPaaS offers no-code or low-code self-delivery capabilities for integrations, effectively coping with complex business scenarios and making it easier for you to quickly integrate systems.

### Does iPaaS store data?

iPaaS currently does not store business data. It only stores integration running logs to help you view the running status and locate problems.

### How do I view running logs?

You can view and switch between real-time monitoring and historical logs in the iPaaS console. You can also specify parameters such as log type and time period to view the logs you want.

### How is the message object of iPaaS designed?

A message is a carrier of runtime data such as metadata in iPaaS and is transferred between components in a flow according to the predefined logic. When a trigger triggers the execution of a flow, it will encapsulate the raw input data into a message and pass it in to a component as parameters. After processing the message, the component will return a new message, which contains the parameters for the next component, and so on until the last component returns the message that contains the return values of the entire flow.
A message consists of the following parts:
A message consists of the body of the message (payload), metadata (attributes), variables, and error content.

### What trigger mechanisms does iPaaS support?

iPaaS currently supports two execution trigger mechanisms: passive data source access triggered at a scheduled time and event-triggered active data source notifications.

### Does iPaaS have a versioning mechanism?

iPaaS provides versioning capabilities. It supports full-lifecycle management from development and deployment to operation and recall based on your integration business requirements.

### How does iPaaS distinguish between the design and operation stages of integration apps?

Each integration app has a status, which can be:
- **Editing**: The app is currently being designed.
- **Running**: The app is currently running.
- **Stopped**: A version which was previously running has been stopped.

An integration app cannot be in both the **Running** and **Editing** statuses at the same time.



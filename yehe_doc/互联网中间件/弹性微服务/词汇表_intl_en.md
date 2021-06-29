
### AS
For more information, please see Auto Scaling.


### Consul
Consul is a highly available distributed system that contains multiple components; therefore, it can provide multiple features. Currently, its main feature is service discovery.


### Service instance
Each individual workload in a service is called a service instance.


### Environment
An environment is an abstract collection of resources and objects. Services in different environments are isolated from each other. Under the premise of network connectivity, services in the same environment can discover and call each other.


### Decoupling
Decoupling refers to breaking the coupling relationship, so that the three layers of data model, business logic, and view display are less coupled with each other, and their mutual dependence and the scope of impact of any potential incident are minimized.


### Auto Scaling
Auto Scaling is a managerial service that automatically adjusts elastic computing resources based on business needs and policies.

### Tencent Cloud Elastic Microservice
Tencent Cloud Elastic Microservice (TEM) is a serverless PaaS platform designed for microservice applications. It perfectly combines serverless resources and the microservice architecture to provide a complete set of out-of-the-box microservice solutions.

### TEM
For more information, please see Tencent Cloud Elastic Microservice.


### Registry
A registry is equivalent to an "address book" in the microservice architecture and is used to record the mapping relationship between services and service addresses. In the distributed architecture, services are registered in the registry, and when a service needs to call other services, it finds the addresses of such services in the registry and call them.

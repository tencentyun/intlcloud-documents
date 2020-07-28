

### Trigger

When you push an image to the specified image repository and Helm Chart, the specified operation is triggered, for example, accessing the specified domain name and transferring basic information about the image repository that generates the trigger.



### Access credential

In Tencent Container Registry (TCR), an access credential refers to the combination of the user name and password used to access instances. The user name is the same as the UIN of the Tencent Cloud user and the password is the temporary password that is generated and is valid within 24 hours by default.

### Access domain name

Each TCR instance has a dedicated access domain name. You can use the Docker client to specify the access domain name for accessing instances and pulling and pushing images.



### Image repository

An image repository is used to store Docker images. One image repository may be associated with one Docker application and manages different versions of the application, that is, Docker images of different versions in the corresponding repository are used to deploy the TCR.



### Namespace

- In TSF of the Tencent microservice platform, a namespace is an abstract set of a group of resources and objects. It is used to isolate resources under one cluster. You can use the same account to create different environments.
  One cluster may have multiple namespaces but resources in a cluster belong to only one namespace. By using namespaces, you can isolate a cluster and divide it into environments such as development environment and test environment.
- In TCR, namespaces are at the directory level inside instances and are equivalent to projects in Organization and Harbor in DockerHub. Namespaces can be used to isolate image repositories in different projects and teams. Namespaces are used between instances and repositories. Their access level attribute directly determines the public and private attributes of internal image repositories. Image repositories and Helm Chart repositories can share namespaces.



### Tencent container registry

Tencent container registry (TCR) is the container image cloud hosting service provided by Tencent Cloud. It supports Docker images, Helm Chart storage and distribution, and secure image scanning and provides enterprise-class customers with fine-grained access permission management and network access control. TCR supports global image synchronization and trigger and meets the requirements of enterprise-class customers for developing global business and using the container CI/CD workflow. It supports large-scale container clusters with thousands of nodes in concurrently pulling GB-level large images and guarantees rapid service deployment. By using TCR, you can enjoy secure and efficient image hosting and distribution services on the cloud without creating or maintaining the image hosting service any more. TCR can also be used with TKE of Tencent Cloud container service (CCS) to obtain smooth experience of CCS.



### Instance

- In the game server engine, an instance is equivalent to a CVM instance and refers to the cloud server provided by the game server engine. For the specific type, check the console of the [Game Server Engine](https://console.cloud.tencent.com/gse/asset).
- On the intelligent titanium machine learning platform, a new instance is generated each time the workflow runs. Instances include historical instances, parameter instances, rerun instances, and timing instances.
- In TCR, an instance consists of one or more related containers that share the same storage and network space.
- In BatchCompute, one instance is equivalent to one CVM instance. Each task can specify one or more instances to execute the task. Instance is the minimum unit of batch scheduling and execution.
- In the data security governance center, an instance generally refers to the unit of data assets on Tencent Cloud. Data assets of different types have different units. For databases, the unit is base; for object storage, the unit is bucket.
- In TCR, instances refer to the exclusive container image hosting services that you can purchase in the specified regions. The backend service and core data storage of instances are independent of the instances of other users. In the original concept of Docker, instances may be equivalent to independent Docker Registry services and can also be understood as follows: users purchase and deploy private Docker Registry services on the cloud.



### TCR

Refer to [Tencent Container Registry](https://intl.cloud.tencent.com/document/product/1051/37244#1367).
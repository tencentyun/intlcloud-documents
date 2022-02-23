## What is CODING Continuous Deployment (CD)?

CODING-CD is a sub-product of [CODING DevOps](https://intl.cloud.tencent.com/zh/products/coding-cd). Continuous deployment is a software development approach in which software functionalities are delivered to a production environment frequently and continuously through automated deployment to ensure the rapid delivery of software products. As an extension of continuous integration, continuous deployment takes advantage of CODING's upstream and downstream products to provide a key process for implementing a closed DevOps loop and ensure end-to-end control.

CODING-CD is used to manage the project release, deployment and delivery processes after build. It can seamlessly connect to upstream Git repositories and downstream artifact repositories to achieve automated deployment. It can also be integrated with webhooks as well as various development and Ops tools. Based on a stable technical architecture and Ops tools, it enables blue/green deployment, grayscale release (canary release), rolling release, and fast rollback.

## Key Features

CODING-CD provides a range of features such as deployment console, cloud account management, permission control, and release orders.

### Deployment console

CODING-CD console is a continuous deployment console implemented based on Spinnaker. It supports multiple cloud services, such as Kubernetes and Tencent Cloud. Users in a DevOps role in the console can manage the list of applications to be deployed, configure deployment pipelines, view and manage application clusters, and perform peer-to-peer operations on clusters (such as scaling, termination, and rollback).

### Permission control

By default, roles and permissions in CODING-CD are as follows:

- Team owner: Has permission to manage deployment.
- Team admin: Has permission to manage deployment.
- Team member: Has no permission to manage deployment.

You can go to **Team Management** > **Permission Configuration** to create user groups and edit their permissions.

### Applications and projects

**Application** is the basic unit of deployment. Applications include functional clusters, security groups, and load balancers. An application also represents a collection of the service you want to deploy, its configuration, and the basic settings required for its operation. It is recommended to match a single application to a service in a microservice architecture
![](https://qcloudimg.tencent-cloud.cn/raw/568b61d70509a97523251a9ad74e1a97.png)

### Cloud account management

Cloud accounts are credentials used to access the cloud platform. On the console homepage, go to **Feature Settings** > **Continuous Deployment** to bind and manage cloud accounts. CODING-CD supports three types of accounts: Kubernetes, Tencent Cloud, and Tencent Cloud TKE. For Kubernetes, Kubeconfig files and Service Account credentials are supported.

Cloud accounts are the basis of continuous deployment. Only after cloud accounts are configured can you perform the deployment on the deployment console by calling the cloud platform APIs.
![](https://qcloudimg.tencent-cloud.cn/raw/862f0d4b214d83e64aa1d1ae22deae80.png)

### Deployment pipeline

A deployment pipeline consists of a series of stages designed to streamline continuous deployment. For basic settings of the cloud platform, CODING-CD allows operations such as deployment, scaling, and disabling. Built-in features such as manual confirmation and webhooks are also available for fine-grained management of continuous deployment workflows.
![](https://qcloudimg.tencent-cloud.cn/raw/3346407ee629522bca59efa7e314f5a4.png)


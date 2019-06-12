## Introduction

### What is Container?
Containers virtualize at the operating system level.  In each individual container, you can run an application, along with its components, in an isolation environment. TKE allows you to package the codes, configuration and dependent components of an application into an easy-to-use building block and controls version, thus improving compatibility, version control, operation efficiency and developers' productivities. TKE promises simple, consist and stable deployment for applications, and stops compatibility problems between applications that reside on the same operating system (OS).
Docker is one of the container platforms, and a Docker container is a basic unit that packages your application with its code, configurations, and dependencies into a single object,  providing isolated environments for running your software services. Here is a figure from the [Official Docker Instruction](https://www.docker.com/what-docker).

![Alt text](https://mc.qcloudimg.com/static/img/3bdd67129c8cee8965898f267d7b881f/Image+057.png)

### What is Tencent Cloud TKE?
Tencent Cloud's Tencent Kubernetes Engines (TKE) is a container management service with high scalability and high performance. You can easily run applications on a hosted CVM instance cluster. With this service, you don't need to install, operate, maintain or expand your cluster management infrastructure. You can enable and disable Docker applications, query all cluster statuses, use various cloud services by calling simple APIs. You can deploy containers in your cluster based on your resource needs and availability requirements, to meet the specific demands of business or applications.

The following concepts help you understand Tencent Cloud's TKE:

- Cluster: A collection of cloud resources required for the container to run, which contains a few CVMs, load balancers, and other Tencent Cloud resources.
- Node: A CVM registered in the cluster.
- Service: A microservice comprised of multiple pods with the same configuration and rules for accessing these pods.
- Batch task: One-time task which contains several pods. The difference between a task and a service is that a task will no longer provide service when stopped.
- Pod: A pod consists of one or more relevant containers, which corresponds to the "pod" of Kubernetes. These containers share the same storage and network.
- Image: Docker image used to deploy TKE. Each image has a unique ID (image's repository address + image name + image Tag).

Their relationship is shown in the figure below:

![Alt text](https://mc.qcloudimg.com/static/img/6ee1f51af42271069c9a46d46731370e/Image+053.png)


### How to Use Tencent Cloud TKE
See the following figure. After creating a cluster, use the image to create a service, enter the service configuration, and wait for the service to be created. You can run the service once it is created successfully.

![Alt text](https://mc.qcloudimg.com/static/img/cb0d84fd7c9547d492ab07f2992093d1/Image+054.png)

- Step 1: Create a cluster
- Step 2: Create a service
- Step 3: View service

Here are the examples that help get started with TKE.

- [Create Simple nginx Service](https://cloud.tencent.com/document/product/457/7851)
- [Create Hello World Node.js Service](https://cloud.tencent.com/document/product/457/7204)
- [Create Wordpress with Single pod](https://cloud.tencent.com/document/product/457/7205)
- [Create Wordpress Service that Uses CDB](https://cloud.tencent.com/document/product/457/7447)

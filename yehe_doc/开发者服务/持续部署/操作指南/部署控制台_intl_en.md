This document describes the console for CODING Continuous Deployment (CODING-CD).

## Prerequisites

You must activate the CODING DevOps service for your Tencent Cloud account before you can use CODING Project Management (CODING-PM). 

## Open Project

1. Log in to the CODING Console and click **Use Now** to go to CODING.
2. On the Workspace homepage, click <img src ="https://main.qcloudimg.com/raw/12230547b45d5eae85ad1c4fa86fba68.png" style ="margin:0" data-nonescope="true"> on the left to go to the CODING-CD Console.

## Function Overview

The CODING-CD Console is built on Spinnaker. It is an integrated control center for managing applications and cloud accounts. In the console, users in an Ops role can manage the list of applications to be deployed, configure deployment pipelines, view and manage application clusters, and perform peer-to-peer operations on clusters (such as scaling, termination, and rollback).

You can open the CODING-CD Console directly from the homepage of your team.

![](https://qcloudimg.tencent-cloud.cn/raw/e35e5a9045096f2cc83442cb8254c178.png)

## Deployment Pipeline

A deployment pipeline consists of a series of **stages** that can streamline continuous deployment. It can be triggered manually or automatically by a CODING Docker repository, webhook, scheduled trigger, etc. In addition, artifacts, parameters, notifications, and serial and parallel logic can be referenced. A **stage** is an automatic build module in the continuous deployment process. You can define the execution sequence of each stage in the pipeline to achieve flexible automated deployment. CODING-CD provides many stage templates to choose from, such as manual confirmation, prerequisite check, and deploy.
![](https://main.qcloudimg.com/raw/2dd250005cfb409cbfadeb7699ed4945.png)

### Deployment Strategy

CODING-CD supports refined deployment strategies, such as red/black (blue/green) deployment, rolling red/black deployment, and grayscale deployment. You can use different deployment strategies for each environment; for example, you can use the red/black strategy in the test environment and the rolling red/black strategy in the production environment. The necessary steps have been encapsulated in the deployment strategy, so that enterprise-grade releases can be implemented without a need for complicated operations.
![](https://main.qcloudimg.com/raw/864a8efd7323bf0c01b65a6af136ed44.png)

## Infrastructure Management

CODING-CD is based on Spinnaker's Clouddriver component, which is compatible with different cloud platforms to implement efficient cloud resource management. The infrastructure consists of the following parts:

- Service group: It is the basic unit of resource management and is used to identify deployable artifacts (such as VM images and Docker images) and configuration items such as the number of instances, auto scaling strategies, and metadata. It may also be associated with load balancers and security groups. After the deployment is complete, it is equivalent to a set of running software instances (e.g., Tencent Cloud auto scaling groups and Kubernetes pods).
- Load balancer: It is used to redirect external network traffic to the running instances in the service group and supports specifying a series of rules to perform health checks on such instances.
- Security group: It defines the network access permissions. A security group rule consists of the IP, port, and communications protocol.
Cluster: It is a logical group of service groups you define.
- Application: It is the basic deployment unit in CODING-CD. Each includes several application clusters as well as load balancers and security groups. It usually represents the services you want to deploy, their configurations, and the basic settings required for their execution. The recommended approach is for one application to correspond to one service in the microservice architecture.

![](https://qcloudimg.tencent-cloud.cn/raw/3baddab1f7807d30a23009ac90703842.png)

## Trigger

While retaining certain native trigger types of Spinnaker, the CODING-CD Console extends trigger types to match CODING upstream artifact repositories.

![](https://qcloudimg.tencent-cloud.cn/raw/396603579fab761f11dbaedaed0d2ad6.png)

## Artifact Type Transformation

While retaining certain native artifact types of Spinnaker, the CODING-CD Console adds support for CODING code repositories in the artifact types of **Git Repository Files**, and CODING Docker image artifacts in the artifact types of **Docker Images**. Such artifact types as War packages and Helm packages are supported.

## Glossary

- Instance: A container or VM instance that is in operation.
- Stack: A user-set custom logic group within a cluster, such as `prod`, `staging`, and `test`.
- Detail: A user-set custom level-3 field that is used to identify a cluster. For example, the service groups with the same `\${Application}-\${Stack}-${Detail}` fields belong to the same cluster.


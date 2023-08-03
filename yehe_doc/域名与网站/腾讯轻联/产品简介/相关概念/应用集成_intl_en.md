Key concepts of iPaaS include integration apps, messages, components, and security gateways. This document describes integration apps.


## Overview
Integration apps are an important capability of iPaaS that make it easier to cope with complex system integrations. For example, a company's internal business systems, including OA, HR, ERP, CRM, and proprietary systems, have independent architectures, which prevents their business logic and data from flowing together easily and makes business processing slow and inefficient. For these complex scenarios, an integration app can be created to interconnect the multiple business systems. You can create multiple integration apps within one project to handle specific integration scenarios. In the above example, an integration app can be created to integrate the OA and HR systems or interconnect the data among the ERP, CRM, and proprietary systems.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/5t9d091_%E5%BA%94%E7%94%A8%E9%9B%86%E6%88%90_02.jpg)


## Components

### Integration apps
An integration app is a way to interconnect systems. You can create an integration app to interconnect data from multiple systems through the use of connectors. Each integration app corresponds to a specific integration scenario. In the above example, the company's large-scale integration includes two integration apps; one is for the OA and HR systems, and the other is for the ERP, CRM, and proprietary systems.

#### Flows

A flow is one of the features used to integrate a single application in a system. An integration app can have one or multiple flows, depending on the business complexity. Flows can be divided into main flows and subflows. The starting node of a main flow must be a trigger [component](https://www.tencentcloud.com/document/product/1165/51576) such as HTTP Listener or Scheduler. The starting node of a subflow isn't necessarily a trigger, and a subflow can be referenced by another flow on a node as a branch to complete a series of data interconnection operations. For example, in the above example, the company's large-scale integration has an integration app for the ERP, CRM, and proprietary systems. The ERP information can be synced to the proprietary systems as the main flow, and sync calls of information between the CRM and ERP systems can run as subflows.


You can orchestrate flows freely on the canvas. You can add different [components](https://www.tencentcloud.com/document/product/1165/51576) on each node as needed to call business system APIs, adapt to protocols, convert data, and implement logics like loop, choice, and concurrency. During flow orchestration, you can also use various debugging capabilities, including app testing, unit testing, and node mock testing, to publish the integration app to the sandbox environment and check whether the input and output of each node are as expected. After debugging, you can publish the integration app to the production environment to start the integration.

### Connector roles
iPaaS is a product in the Tencent Cloud console. It can be logged in to with a Tencent Cloud account and supports access management through [CAM](https://www.tencentcloud.com/document/product/598). You can be redirected to CAM from the iPaaS console to add sub-accounts under your Tencent Cloud root account, and iPaaS will automatically pull all sub-accounts under the root account to the member list. For example, ordinary member A has read/write permissions for the integration app for the OA and HR systems, while ordinary member B has the read-only permission for the same integration app.

The system admin and project admin can add a user to a project so the user can participate in co-development of integration apps. The system admin can grant an ordinary user the project admin privileges or revoke the privileges. The system admin and project admin can both grant ordinary users read-only permission or read/write permission for specified integration apps within the project.

#### System admin
A system admin has the highest privileges of iPaaS. A Tencent Cloud root account automatically has system admin privileges which cannot be revoked. A system admin can grant any member the system admin and project admin privileges or revoke the privileges. They can also grant ordinary users in a project the read-only permission or read/write permissions for a specified integration app within the project.

#### Project admin
A project admin can grant or revoke the project admin privileges and grant any users in the integration project the read-only permission or read/write permissions for specified integration apps.

#### Ordinary member
All sub-accounts under a Tencent Cloud root account will automatically become ordinary members in iPaaS.

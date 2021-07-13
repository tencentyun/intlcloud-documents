## Overview

This document describes how to create an application and deploy it in the TEM console.

## Prerequisites

1. You have already [created an environment](https://cloud.tencent.com/document/product/1371/53293).
2. You have [added environment resources](https://cloud.tencent.com/document/product/1371/55684) (choose log service, storage service, or registry as needed).

## Directions

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem).
2. On the left sidebar, click **Application List** to enter the application list page and select your application deployment region.

| Region | AZs Supported for Deployment |
| ---- | ---------------------- |
| Guangzhou | Zones 3, 4, and 6 |
| Shanghai | Zones 2, 3, 4, and 5 |

3. Click **Create** to access the application creation page and enter the application information.
   ![](https://main.qcloudimg.com/raw/fbf88fef630b27b88fa0a4f2ddaff25c.png)

   - Name: enter the application name, which can contain up to 45 lowercase letters, digits, and hyphens and cannot start or end with a hyphen.
   - Programming Language: select your programming language.
   - Package Upload Method: select a package upload method. The Java language supports uploading images, JAR packages, and WAR packages, while other languages only support uploading images. If you select **JAR package** or **WAR package**, TEM will automatically build a container image for you and push it to your personal container image repository created by TEM.

4. Click **Submit** and select **OK** in the pop-up window to enter the application deployment page. If you select **Cancel**, you can click **Deploy to New Environment** in the application list to complete the application deployment later.
   <img src="https://main.qcloudimg.com/raw/2cfd50d64227a7ae589eb8203f512c58.png">
5. On the application deployment page, configure the relevant parameters according to the specific conditions of your application.
   ![](https://main.qcloudimg.com/raw/a84a9d3b433b6fa8d3e9ed297ed4b178.png)

   The parameters are described as follows:
	

   | Parameter | Description |
   | --------------- | ------------------------------------------------------------ |
   | Release Environment | Select the environment where the application is located. If there are no suitable environments, you can create one on the [Environment](https://console.cloud.tencent.com/tem/env) page as instructed in [Creating Environment](https://cloud.tencent.com/document/product/1371/53293). |
   | JDK Version | Select the JDK version, which can be OpenJDK 8 or KonaJDK 8. |
   | Upload Package/Image | Upload your package or image or download the demos in the console to deploy them and try out all the features of TEM. |
   | Version Number | Set the application version number. You can choose to enter the version number or click **Use Timestamp as Version Number** to use the timestamp as the application version number. |
   | Version Description | Enter the version description. |
   | Launch Parameter | Set the launch parameter. |

>?If your service is in Java and associated with a registry, TEM will be able to automatically inject the registry information. For more information, please see [Service Registration and Discovery](https://cloud.tencent.com/document/product/1371/56367).

6. (Optional) You can set the following advanced options as needed:


| Parameter | Required | Description |
| ---------- | -------- | ------------------------------------------------------------ |
| Resource Configuration | Yes | You can set a number manually or set an auto scaling rule to automatically scale. |
| Access Configuration | No | <li>Access Method: access within the environment. The public network access can be configured globally in [Environment](https://console.cloud.tencent.com/tem/env). For more information, please see [Configuring Application Access and Routing](https://cloud.tencent.com/document/product/1371/55685). </li><li>Protocol: TCP and UDP protocols are supported. When public network/private network CLB instances are used, TCP and UDP protocols cannot be used together. </li> |
| Environment Variables | No | Configure environment variables. |
| <nobr>Persistent Storage</nobr> | No | Persistent Storage: provide storage for the container. Currently, CFS is supported, which needs to be mounted to the specified path of the container. <li>Data Volume: add the CFS storage resources associated in [Adding Environment Resource](https://cloud.tencent.com/document/product/1371/55684). </li><li>Mount Target: select the target path to mount the data volume added in this step and enter the version description. </li> |
| Security Group | No | You can configure a security group rule to allow or reject the outbound and inbound traffic of instances in the security group. If you need to open other ports for your business, you can [create a security group](https://console.cloud.tencent.com/vpc/securitygroup) accordingly. |
| Log Configuration | No | You can enable **Persistent storage in CLS**. This supports standard output `stdout` and `*` configuration paths such as `/logs/*`, which should be separated by commas. Standard output is used by default. |

7. Click **Submit** to complete the application deployment.
8. For microservice applications, the steps to deploy consumer and server applications are similar to steps 3–7.

## Application Access

TEM provides two ways of access: intra-environment access and public network access.

- Intra-environment access: microservices in the same environment can call each other through the registered service names. Service registration and discovery based on registries such as Consul and Eureka as well as service discovery based on Kubernetes are supported.
- Public network access: click the **Environment** block and create public network CLB instances and HTTP/HTTPS forwarding rules on the **Access Configuration** page to access the application.

Taking public network access as an example, the steps are as follows:
1. Create a public network access route as instructed in [Configuring Application Access and Routing](https://cloud.tencent.com/document/product/1371/52886).
2. Click the ID of the application to enter the instance list page.
3. Select **Basic Info** at the top of the page. Then, in the **Access Configuration** module, you can view the domain name and path for accessing the application.
	![](https://main.qcloudimg.com/raw/bfb77deab6549a5c2f4ef908fc7ef133.png)
4. Enter the following URL in a browser:
  ```xml
   <public network access address/domain name>+<path>
  ```
   For example, enter `http://xx.xx.xx.xx/ping-provider`, and if the following result is returned, the application is deployed successfully:
   ```
   Hello World!
   ```




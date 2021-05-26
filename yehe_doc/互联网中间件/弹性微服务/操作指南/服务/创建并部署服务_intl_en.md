## Overview

This document describes how to create a service and deploy it in the TEM console.

## Directions

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem).
2. On the left sidebar, click **Service List** to enter the service list page and select your service deployment region.
3. Click **Create** to access the service creation page and enter the service information.
   ![](https://main.qcloudimg.com/raw/a734a55c6c2c98294fa9da59efc873b5.png)
   - Name: enter a service name.
   - Programming Language: select your programming language.
   - Package Upload Method: select a package upload method. The Java language supports uploading images, JAR packages, and WAR packages, while other languages only support uploading images. If you select **JAR package** or **WAR package**, TEM will automatically build a container image for you and push it to your personal container image repository created by TEM.
4. Click **Next** to enter the deployment service version page. Please configure the relevant parameters according to the specific conditions of your service.
>?You can click the following tab to view the configuration instructions for the corresponding deployment method.
<dx-tabs>
::: Package deployment
![](https://main.qcloudimg.com/raw/c3603c05adec131576fb1a46d6559b60.png)
- JDK Version: select **Open JDK 8** or **Kona JDK 8**.
- Upload Package: upload your package or download the demo and upload and deploy it to try out all the features of TEM.
- Release Environment: select the environment where the service is located. If there are no suitable environments, you can create one on the [Environment](https://console.cloud.tencent.com/tem/env) page as instructed in [Creating Environment](https://intl.cloud.tencent.com/document/product/1094/40358).
- Number of Instances: set a number manually or set an auto scaling rule to automatically scale.
- Service Port: enter the port number that the service listens on. If you use demo packages, the corresponding ports are as follows:
 JAR package demo port number: 8201; WAR package demo port number: 8080.
- Environment Variables: configure environment variables.
- Persistent Storage: provide storage for the container. Currently, CFS is supported, which needs to be mounted to the specified path of the container.
 - Data Volume: add the CFS storage resources associated in [Adding Environment Resource](https://intl.cloud.tencent.com/document/product/1094/40361).
 - Mount Target: select the target path to mount the data volume added in this step.
- Security Group: you can configure a security group rule to allow or reject the outbound and inbound traffic of instances in the security group. If you need to open other ports for your business, you can [create a security group](https://console.cloud.tencent.com/vpc/securitygroup) accordingly.
- Log Configuration: you can enable **Persistent storage in CLS**. This supports standard output `stdout` and `*` configuration paths such as `/logs/*`, which should be separated by commas. Standard output is used by default.
:::
::: Image deployment
![](https://main.qcloudimg.com/raw/00d8a7925db75c66ba6f422f4d94cf0d.png)
- Image Source: you can choose to upload your own image or directly deploy the demo image to try out all the features of TEM.
- Release Environment: select the environment where the service is located. If there are no suitable environments, you can create one on the [Environment](https://console.cloud.tencent.com/tem/env) page as instructed in [Creating Environment](https://intl.cloud.tencent.com/document/product/1094/40358).
- Number of Instances: set a number manually or set an auto scaling rule to automatically scale.
- Service Port: enter the port number that the service listens on. If you use the demo image, the port number is automatically populated.
- Environment Variables: configure environment variables.
- Persistent Storage: provide storage for the container. Currently, CFS is supported, which needs to be mounted to the specified path of the container.
 - Data Volume: add the CFS storage resources associated in [Adding Environment Resource](https://intl.cloud.tencent.com/document/product/1094/40361).
 - Mount Target: select the target path to mount the data volume added in this step.
- Security Group: you can configure a security group rule to allow or reject the outbound and inbound traffic of instances in the security group. If you need to open other ports for your business, you can [create a security group](https://console.cloud.tencent.com/vpc/securitygroup) accordingly.
- Log Configuration: you can enable **Persistent storage in CLS**. This supports standard output `stdout` and `*` configuration paths such as `/logs/*`, which should be separated by commas. Standard output is used by default.
:::
</dx-tabs>
5. Click **Submit** to complete the creation.


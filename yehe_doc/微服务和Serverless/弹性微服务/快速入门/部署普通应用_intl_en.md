## Overview

This document describes how to deploy a JAR package of the JAVA Demo sample application on Tencent Cloud Elastic Microservice and enable its public network access.

## Prerequisites

Please make sure that you have read and completed the [preparations](https://intl.cloud.tencent.com/document/product/1094/41383) before starting to deploy your application.


## Directions

### Step 1: obtain the demo application

This document uses the demo application developed in Java Spring Boot as an example. [Click here to download the JAR package](https://tem-demo-1254962064.cos.ap-shanghai.myqcloud.com/hello-world-0.0.1-SNAPSHOT.jar).



### Step 2: deploy the application

1. Select the application deployment region at the top of the **[Application Management](https://console.cloud.tencent.com/tem/application)** page in the TEM console.
2. Click **Create** to access the **New application** page and enter the application information.
     ![](https://main.qcloudimg.com/raw/ee456bf7ffe1fe15554ec3399df840fe.png)
3. Select **Programming Language** and **Package Upload Method** for your application.
   - Image, JAR, and WAR files can be uploaded in Java, while only image files can be uploaded in other languages.
   - If you select **Image > Auto Create** for package upload, the image you upload will be pushed to the **namespace** created automatically by TEM.
   - If you select **JAR** or **WAR** for package upload, TEM will automatically build a container image for you and push it to the **namespace** created by TEM.
>?If you have not configured **Tencent Container Registry**, or an error occurs after you click **Next**, [activate the TCR service](https://intl.cloud.tencent.com/document/product/1094/41386).

4. Click **Submit** and then click **OK** in the pop-up window to go to the application deployment page.
5. On the **Deploy Application** page, configure the relevant parameters as needed.
   ![](https://main.qcloudimg.com/raw/5cde618b2418fca282ad75ac56f8dcd0.png)
   - **Upload Package**: upload your application package.
   - **Release Environment**: select the environment just created.
   - If you need to configure other advanced options for your application, please see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
6. Click **Deploy**.



### Step 3: access the application

After your application is deployed successfully, you need to create an access configuration for it, so that it can be accessed over the public network.

1. Select the application deployment region at the top of the **[Environment](https://console.cloud.tencent.com/tem/env)** page in the TEM console.

2. Click the environment where your application is deployed to enter the details page and select **Access Configuration** at the top.

3. Click **Create** to access the **Create Access Configuration** page to configure the access information.
   ![](https://main.qcloudimg.com/raw/7a960a81645810e39cefe7c969b08996.png)

   - **Network Type**: check **Public Network**. To configure an intra-environment access, please see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
   - **Load Balancer**: check **Automatically create**.
   - **Protocol & Port**: HTTP:80 and HTTPS:443 are supported, and HTTPS domain names can be bound to certificates. Select HTTP:80 for the Demo application.
   - **Forwarding Configuration**:
     - Domain Name: existing domain names can be bound. If there are no domain names, you will be assigned an IPv4 IP by default. For the demo application, use the assigned default IP address.
     - **Path**: it defaults to “/”. Configure it as needed.
     - Backend Application: select the demo application you deployed.
     - Application Port: for the demo application, use port 8201.
   - **Server Certificate**: if the HTTP protocol is selected, you need to select a server certificate. If existing certificates are not suitable, you can [create one](https://console.cloud.tencent.com/clb/cert).

4. Click **OK** to complete the new access configuration. Then you can view the public network access IP of the application under the **Access Configuration** section of the environment details page.
   ![](https://main.qcloudimg.com/raw/750e0fa57660b8b13f84ae439032b056.png)

5. Enter the public network access IP in a browser. If the following result is returned, the application has been successfully deployed.

   ```plaintext
   	Hello World!
   ```

## Overview

This document describes how to deploy a JAR package of the JAVA Demo sample application on Tencent Cloud Elastic Microservice and enable its public network access.

## Preparation

You have created an environment and application.

## Directions

### Step 1: Obtain the demo application
This document uses the demo application developed in Java Spring Boot as an example. [Click here to download the JAR package](https://tem-demo-1254962064.cos.ap-shanghai.myqcloud.com/hello-world-0.0.1-SNAPSHOT.jar).



### Step 2: Deploy the application
1. On the **Application management** page, select the target application and click **Deploy to new environment**.
![](https://qcloudimg.tencent-cloud.cn/raw/7cacf350dd2e2b5f9254ae4c70c2c0eb.png)
2. On the **Deploy Application** page, configure the relevant parameters as needed.
   ![](https://qcloudimg.tencent-cloud.cn/raw/990076d27631a9d7c79544bec0490065.png)
   - Upload Package: Upload your package.
   - **Release Environment**: Select the environment just created.
   - If you need to configure other advanced options for your application, see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
3. Click **Deploy**.



### Step 3: Access the application

After your application is deployed successfully, you need to create an access configuration for it, so that it can be accessed over the public network.

1. Select the application deployment region at the top of the [**Environment**](https://console.cloud.tencent.com/tem/env) page in the TEM console.
2. Click the environment where your application is deployed to enter the details page and select **Access configuration** at the top.
3. Click **Create** to go to the access configuration creation page and enter the access configuration information.
   ![](https://main.qcloudimg.com/raw/7a960a81645810e39cefe7c969b08996.png)
   
   - **Network Type**: Select **Public Network**. To configure an intra-environment access, see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
   - **Load Balancer**: Select **Automatically create**.
   - **Protocol & port**: `HTTP:80` and `HTTPS:443` are supported, and HTTPS domain names can be bound to certificates. Select `HTTP:80` for the demo application.
   - **Forwarding Configuration**:
     - Domain Name: Existing domain names can be bound. If there are no domain names, you will be assigned an IPv4 IP by default. For the demo application, use the assigned default IP address.
     - **Path**: It defaults to "/". Configure it as needed.
     - Backend Application: Select the demo application you deployed.
     - Application Port: For the demo application, use port 8201.
   - **Server Certificate**: If the HTTP protocol is selected, you need to select a server certificate. If existing certificates are not suitable, you can [create one](https://console.cloud.tencent.com/clb/cert).
4. Click **OK**. You can view the public IP of the application under **Access configuration** on the **Environment details** page.
![](https://main.qcloudimg.com/raw/750e0fa57660b8b13f84ae439032b056.png)
5. Enter the public IP of the application in a browser. If the following result is returned, the application is successfully deployed.
   ```plaintext
   	Hello World!
   ```

## Overview

This document describes how to deploy a JAR package of the JAVA Demo sample application on Tencent Cloud Elastic Microservice and enable its public network access.

## Prerequisites

Create an environment and application.

## Directions

### Step 1. Get the Demo
This document uses the demo application developed in Java Spring Boot as an example. [Click here to download the JAR package](https://tem-demo-1254962064.cos.ap-shanghai.myqcloud.com/hello-world-0.0.1-SNAPSHOT.jar).



### Step 2. Deploy the Application
1. On the **Application management** page, select the target application and click **Deploy to new environment**.
![](https://qcloudimg.tencent-cloud.cn/raw/7cacf350dd2e2b5f9254ae4c70c2c0eb.png)
2. On the **Deploy Application** page, configure the relevant parameters as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/990076d27631a9d7c79544bec0490065.png)
   - Upload Package: upload your package.
   - **Release Environment**: select the environment just created.
   - If you need to configure other advanced options for your application, please see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
6. Click **Deploy**.



### Step 3. Access the Application

After the deployment, you need to create a configuration for it in the CLB gateway for internet access.

1. In the TEM console, click [CLB Gateways](https://console.cloud.tencent.com/tem/gateway?rid=33) in the left sidebar.  
2. Click **Create** and enter the gateway configuration. Choose the correct **Environment**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/y5d9759_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230104103532.png)
   
   - **Network Type**: Select **Public Network**. To configure an intra-environment access, see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
   - **Load balancer**: Create one automatically or use an existing CLB.
   - **Protocol & port**: **HTTP:80** and **HTTPS:443** are supported, and HTTPS domain names can be bound to certificates. Select **HTTP:80** for the Demo application.
   - **IP version**: Options include **IPv4** and **IPv6 NAT64**.
   - **Forwarding configuration**:
     - **Domain name**: Choose an existing domain name. If it’s not specified, a random IPv4 IP is assigned by default. For the demo application, use the assigned default IP address.
     - **Path**: It defaults to “/”. Configure it as needed.
     - **Backend application**: Select the demo application.
     - **Application port**: For the demo application, use port 8201.
   - **Server certificate**: If **HTTP** is selected, you need to select a server certificate. If existing certificates are not suitable, you can [create one](https://console.cloud.tencent.com/clb/cert).
4. Click **Confirm** to complete the configuration. You can then check the IP for internet access in the list of CLB gateways.
![](https://main.qcloudimg.com/raw/750e0fa57660b8b13f84ae439032b056.png)
5. Enter the public IP of the application in a browser. If the following result is returned, the application is successfully deployed.
   ```plaintext
   	Hello World!
   ```

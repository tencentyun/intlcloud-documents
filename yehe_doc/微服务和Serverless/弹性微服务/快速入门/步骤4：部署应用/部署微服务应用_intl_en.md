## Overview

This document describes how to deploy your microservice applications in TEM and make them mutually callable and accessible over the public network by using the provider/consumer demo applications developed in Spring Cloud with JAR file upload as an example.

## Preparation

You have created an environment and application.

## Directions

### Step 1: Obtain the demo application

TEM currently supports Nacos, Eureka, and ZooKeeper registries. The following steps take the Eureka registry as an example. To demonstrate Spring Cloud microservice applications using a registry, we have prepared a set of provider/consumer demo applications using the Eureka registry. You can view their source code at [GitHub](https://github.com/tencentyun/tem-demo) or directly download them as JAR packages.

 Demo applications with the Eureka registry: [provider demo](https://tem-demo-1254962064.cos.ap-shanghai.myqcloud.com/eureka-provider-0.0.1-SNAPSHOT.jar) and [consumer demo](https://tem-demo-1254962064.cos.ap-shanghai.myqcloud.com/eureka-consumer-0.0.1-SNAPSHOT.jar).


### Step 2. Configure a registry

Before you start to deploy the Spring Cloud demo application, you need to configure the **registry** resource in the **environment**. Add the registry corresponding to the application you select as instructed in [Adding Environment Resources](https://intl.cloud.tencent.com/document/product/1094/40361).



### Step 3. Deploy the application

1. On the **Application management** page, select the target application and click **Deploy to new environment**.
![](https://qcloudimg.tencent-cloud.cn/raw/7cacf350dd2e2b5f9254ae4c70c2c0eb.png)
2. On the **Deploy Application** page, configure the relevant parameters as needed.
   ![](https://qcloudimg.tencent-cloud.cn/raw/990076d27631a9d7c79544bec0490065.png)
   - Upload Package: Upload your package.
   - **Release Environment**: Select the environment just created.
   - For a Spring Cloud application, if a **registry** is associated with the selected **release environment**, you can select **Auto Inject Registry Info**. For detailed directions of registration and discovery, see [Application Registration and Discovery](https://intl.cloud.tencent.com/document/product/1094/40960).
   - If you need to configure other advanced options for your application, see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
3. Click **Deploy** to complete the deployment of the provider application.
4. Repeat **steps 1–3** to complete the deployment of the consumer application.



### Step 4. View the registered applications

1. After the application instance to be deployed starts running, you can enter the [Registry](https://console.cloud.tencent.com/tse/zookeeper) page in the TEM console and select the registry associated with your deployment environment.
2. On the registry details page, select the **Application Management** tab to check whether the provider and consumer applications are successfully registered.
   

### Step 5. Verify the access

The provider/consumer applications that have been successfully deployed and registered can be accessed over the public network by creating an access configuration in the **environment** for the consumer application.
<img src="https://qcloudimg.tencent-cloud.cn/raw/2aed6ac69e638b09e6b010083697ec26.png" width="100%">

1. Select the application deployment region at the top of the [**Environment**](https://console.cloud.tencent.com/tem/env) page in the TEM console.
2. Click **View Details** in the block of the environment where your application is deployed to enter the details page and select **Access Management** at the top.
3. Click **Create** to go to the access configuration creation page and enter the access configuration information.
   ![](https://main.qcloudimg.com/raw/7a960a81645810e39cefe7c969b08996.png)
   
   - Network type: Public network. If you need intra-environment access, see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
   - **Load Balancer**: Select **Automatically create**.
   - **Protocol & Port**: HTTP:80 and HTTPS:443 are supported, and HTTPS domain names can be bound to certificates. Select HTTP:80 for the Demo application.
   - **Forwarding Configuration**:
     - Domain Name: Existing domain names can be bound. If there are no domain names, you will be assigned an IPv4 IP by default. For the demo application, use the assigned default IP address.
     - **Path**: It defaults to "/". Configure it as needed.
     - Backend Application: Select the consumer demo application you deployed.
     - Application Port: For the eureka-consumer application, use port 8003.
   - **Server Certificate**: If the HTTP protocol is selected, you need to select a server certificate. If existing certificates are not suitable, you can [create one](https://console.cloud.tencent.com/clb/cert).
4. Click **OK**. You can view the public IP of the application under **Access management** on the **Environment details** page.
   ![](https://main.qcloudimg.com/raw/750e0fa57660b8b13f84ae439032b056.png)
5. Enter the following URL in a browser:
   ```plaintext
   http://public IP/ping-provider
   ```
   If the following result is returned, the application is successfully deployed:
   ```plaintext
   pong from eureka-provider 
   ```

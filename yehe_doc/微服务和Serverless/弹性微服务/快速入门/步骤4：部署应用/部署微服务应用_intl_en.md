## Overview

This document describes how to deploy your microservice applications in TEM and make them mutually callable and accessible over the public network by using the provider/consumer demo applications developed in Spring Cloud with JAR file upload as an example.

## Prerequisites

Create an environment and application.

## Directions

### Step 1. Get the demo application

TEM currently supports Nacos, Eureka (for existing users), and ZooKeeper registries. The following steps take the Nacos registry as an example. To demonstrate Spring Cloud microservice applications using a registry, we have prepared a set of provider/consumer demo applications using the Nacos registry. You can view their source code at [GitHub](https://github.com/tencentyun/tse-simple-demo) or directly download them as JAR packages.

 Nacos registry Demo application: [Provider Demo](https://tem-demo-1305738457.cos.ap-shanghai.myqcloud.com/nacos-provider-demo-2.0.1.RELEASE.jar) and [Consumer Demo](https://tem-demo-1305738457.cos.ap-shanghai.myqcloud.com/nacos-consumer-demo-2.0.1.RELEASE.jar)。


### Step 2. Configure the Registry

Before you start to deploy the Spring Cloud demo application, you need to configure the **registry** resource in the **environment**. Please add the registry corresponding to the application you select as instructed in [Adding Environment Resource](https://intl.cloud.tencent.com/document/product/1094/40361).


### Step 3. Deploy the Application

1. On the **Application management** page, select the target application and click **Deploy to new environment**.
![](https://qcloudimg.tencent-cloud.cn/raw/7cacf350dd2e2b5f9254ae4c70c2c0eb.png)
2. On the **Deploy Application** page, configure the relevant parameters as needed.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/gNJD139_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230104104641.png)
   - Upload Package: upload your package.
   - **Release Environment**: select the environment just created.
   - For information about advanced options, see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
3. For a Spring Cloud application, if a registry is associated with the selected **release environment**, you can select **Auto Inject Registry Info**. For more information, see [Application Registration and Discovery](https://intl.cloud.tencent.com/document/product/1094/40960).
4. Click **Deploy** to complete the deployment of the consumer application.
5. Repeat the four steps above to deploy the provider application.



### Step 4. Check Registered Applications

1. After the application instance to be deployed starts running, you can enter the [Registry](https://console.cloud.tencent.com/tse/zookeeper) page in the TEM console and select the registry associated with your deployment environment.
2. On the registry details page, select the **Application Management** tab to check whether the provider and consumer applications are successfully registered.



### Step 5. Verify the Access

After deployment of the provider and consumer applications, you can create an access configuration in the **CLB gateway** for the consumer application for internet access.
<img src="https://qcloudimg.tencent-cloud.cn/raw/2aed6ac69e638b09e6b010083697ec26.png" width="80%">

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
     - **Backend application**: Select the consumer demo application you deployed.
     - **Application port**: Select port 19003 for the consumer demo application.
   - **Server certificate**: If **HTTP** is selected, you need to select a server certificate. If existing certificates are not suitable, you can [create one](https://console.cloud.tencent.com/clb/cert).
4. Click **Confirm** to complete the configuration. You can then check the IP for internet access in the list of CLB gateways.
![](https://main.qcloudimg.com/raw/750e0fa57660b8b13f84ae439032b056.png)
5. Enter the following URL in a browser:
   ```plaintext
   http://IP for internet access/echo/str
   ```
   If the following result is returned, the application is successfully deployed.
   ```plaintext
   Hello Nacos Provider str
   ```

## Overview
This document describes how to deploy a JAR package of the JAVA Demo sample application on Tencent Cloud Elastic Microservice and enable its public network access.

## Prerequisites
Before deploying your applications, you have completed the [preparations](https://intl.cloud.tencent.com/document/product/1094/41383).


## Directions
### Step 1: obtain the Demo application.

[Click to download a JAR package](https://tem-demo-1254962064.cos.ap-shanghai.myqcloud.com/hello-world-0.0.1-SNAPSHOT.jar) of the Demo application developed using Java Spring Boot.



### Step 2: deploy the application

1. Log in to the TEM console, access the [**Application Management**](https://console.cloud.tencent.com/tem/service) page, and select a region to deploy the application.
2. Click **Create** to access the **New application** page and enter the application information.
  ![](https://main.qcloudimg.com/raw/ee456bf7ffe1fe15554ec3399df840fe.png)
3. Select **Programming Language** and **Package Upload Method** for your application.
   - The Java language supports uploading images, JAR packages, and WAR packages, while other languages only support uploading images.
   - If you choose to upload the application using **Image > Automatically create**, the image you uploaded will be pushed to a **namespace** automatically created by TEM.
   - If you choose to upload the application using **JAR package** or **WAR package**, TEM will automatically build a container image for you and push the package to an auto-created **namespace**.
>?If you did not configure **Tencent Container Registry** or receive an error message after clicking **Next**, [activate the TCR service](https://intl.cloud.tencent.com/document/product/1094/41386).
>
4. Click **Submit** and then click **OK** in the pop-up window to go to the application deployment page.
5. On the **Deploy Application** page, configure the relevant parameters as needed.
![](https://main.qcloudimg.com/raw/5cde618b2418fca282ad75ac56f8dcd0.png)
	- **Upload Package**: upload your application package.
	- **Release Environment**: select the environment just created.
	- If your application requires advanced configurations, see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
6. Click **Deploy**.



### Step 3: access the application

After deploying the application, create an access configuration in the environment to access it via the public network.

1. Log in to the TEM console, access the [**Environment**](https://console.cloud.tencent.com/tem/env) page, and select the region where the application has been deployed.
2. Select the target environment and click **Access Configuration** at the top of the details page.
3. Click **Create** to access the **Create Access Configuration** page to configure the access information.
![](https://main.qcloudimg.com/raw/7a960a81645810e39cefe7c969b08996.png)
	- **Network Type**: check **Public Network**. To configure an intra-environment access, please see [Creating and Deploying Application](https://intl.cloud.tencent.com/document/product/1094/40362).
	- **Load Balancer**: check **Automatically create**.
	- **Protocol & Port**: HTTP:80 and HTTPS:443 are supported, and HTTPS domain names can be bound to certificates. Select HTTP:80 for the Demo application.
	- **Forwarding Configuration**:
		- **Domain name**: choose an existing domain name (if any) to bind. Otherwise, you will be assigned an IPv4 address by default. Use the system-assigned IPv4 address for the Demo application.
		- **Path**: it defaults to “/”. Configure it as needed.
		- **Backend Application**: choose the Demo application you’ve deployed.
		- **Application Port**: enter the port 8201 for the Demo application.
	- **Server Certificate**: if the HTTP protocol is selected, you need to select a server certificate. If existing certificates are not suitable, you can [create one](https://console.cloud.tencent.com/clb/cert).
4. Click **OK** to complete the new access configuration. Then you can view the public network access IP of the application under the **Access Configuration** section of the environment details page.
	 	 ![](https://main.qcloudimg.com/raw/750e0fa57660b8b13f84ae439032b056.png)
5. Enter the public network access IP in a browser. If the following result is returned, the application has been successfully deployed.
    ```plaintext
		Hello World!
	```



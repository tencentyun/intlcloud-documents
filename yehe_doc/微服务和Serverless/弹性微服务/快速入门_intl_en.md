This document describes how to deploy and access an application in the TEM console.

## Prerequisites

You have successfully applied for [TEM beta test](https://intl.cloud.tencent.com/apply/p/wqinnd8p97) eligibility so that you can access the TEM console. If you do not have a Tencent Cloud account, please sign up for one by referring to [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).

## Directions

### Step 1. Create an environment

1. Log in to the [TEM Console](https://console.cloud.tencent.com/tem).
2. On the **Environment** page, select a deployment region and click **Create**.
3. Configure the environment information.
   ![](https://main.qcloudimg.com/raw/454560d35dec94352c9a7dc8885e1f35.png)
   - Name: enter up to 40 characters.
   - VPC: select an existing VPC. If your existing VPCs are not suitable or you haven't created a VPC yet, you can click [Create VPC](https://console.cloud.tencent.com/vpc/vpc?rid=4) to create one (**the selected region must be the same as that of the environment**), return to and refresh this page, and select it.
   - Subnet: select an existing subnet. We recommend you choose multi-AZ deployment to improve the disaster recovery capabilities. If your existing subnets are not suitable or you haven't created a subnet yet, you can click [Create Subnet](https://console.cloud.tencent.com/vpc/subnet?rid=4&unVpcId=) to create one, return to and refresh this page, and select it.
   - CoreDNS is automatically deployed to support service discovery in the environment. Specifically, two replica nodes of `Deployment:coredns` are automatically deployed in the Kubernetes cluster namespace `kube-ststem`. This service is free of charge, and we recommend you not modify it.
4. Click **OK** and the environment will enter the initialization status. It will be created a few minutes later.

### Step 2. Create an application

1. On the left sidebar, click **Application List** to enter the application list page and select a deployment region for your application.

2. Click **Create** to access the application creation page and enter the application information.
   ![](https://main.qcloudimg.com/raw/b6c1223c58aed0e9a55de58907be4d33.png)

   - Name: enter the application name.
   - Programming Language: select your programming language.
   - Package Upload Method: select a package upload method. The Java language supports uploading images, JAR packages, and WAR packages, while other languages only support uploading images. If you select **JAR package** or **WAR package**, TEM will automatically build a container image for you and push it to your personal container image repository created by TEM.

3. Click **Submit** and select **OK** in the pop-up window to enter the application deployment page. If you select **Cancel**, you can click **Deploy to New Environment** in the application list to complete the application deployment later.

   ![](https://main.qcloudimg.com/raw/e6a50706b5bfbb740efcb764aea8819c.png)

### Step 3. Deploy the application

1. On the application deployment page, configure the relevant parameters according to the specific conditions of your application.
   ![](https://main.qcloudimg.com/raw/ef719950af4ec344445967fe0c28522d.png)

   Parameter description

   | Parameter | Description |
   | :-------------- | :----------------------------------------------------------- |
   | Release Environment | Select the environment you created. |
   | JDK Version | Select the JDK version, which can be OpenJDK 8 or KonaJDK 8. |
   | Upload Package/Image | Upload your package or image or download the demos in the console to deploy them and try out all the features of TEM. |
   | Version Number | Set the application version number. You can choose to enter the version number or click **Use Timestamp as Version Number** to use the timestamp as the application version number. |
   | Version Description | Enter the version description. |
   | Start Parameter | Set the start parameter. |

2. Click **Submit** to complete the application deployment.

### Step 4. Access the application

TEM provides two ways of access: intra-environment access and public network access.

- Intra-environment access: microservices in the same environment can call each other through the registered service names. Service registration and discovery based on registries such as Consul and Eureka as well as service discovery based on Kubernetes are supported.
- Public network access: click the **Environment** block and create public network CLB instances and HTTP/HTTPS forwarding rules on the **Access Configuration** page to access the application.

Taking public network access as an example, the steps are as follows:

1. Click the environment block to go to the **Access Configuration** page, and click **Create** to create a public network access route.

   ![](https://main.qcloudimg.com/raw/952032dd3b7ccb822dfc75a539db2bbf.png)
   
2. Enter the following URL in a browser:

   ```xml
   <public network access address/domain name>+<path>
   ```

   For example, if the following result is returned after you enter `http://xx.xx.xx.xx/ping-provider`, the application is deployed successfully.

   ```
   Hello World！
   ```

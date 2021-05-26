The process of using TEM is as follows:

![](https://main.qcloudimg.com/raw/63da7398f0c41a3b9758b922182a1205.png)

### Step 1. Log in to the console

Apply for the closed beta test qualification for TEM and access the console after your application is approved. If you don't have an account yet, please register as instructed in [Signing up for a Tencent Cloud Account](https://intl.cloud.tencent.com/document/product/378/17985).

### Step 2. Create an environment

1. Log in to the [TEM console](https://console.cloud.tencent.com/tem).
2. On the **Environment** page, select a deployment region and click **Create**.
3. Configure the environment information.
   ![](https://main.qcloudimg.com/raw/ded33af03ca47e9206e83a92950321b3.png)
   - Name: enter up to 40 characters.
   - VPC: select an existing VPC. If your existing VPCs are not suitable or you haven't created a VPC yet, you can click [Create VPC](https://console.cloud.tencent.com/vpc/vpc?rid=4) to create one (**the selected region must be the same as that of the environment**), return to and refresh this page, and select it.
   - Subnet: select an existing subnet. We recommend you choose multi-AZ deployment to improve the disaster recovery capabilities. If your existing subnets are not suitable or you haven't created a subnet yet, you can click [Create Subnet](https://console.cloud.tencent.com/vpc/subnet?rid=4&unVpcId=) to create one, return to and refresh this page, and select it.
   - CoreDNS is automatically deployed to support service discovery in the environment. Specifically, two replica nodes of `Deployment:coredns` are automatically deployed in the Kubernetes cluster namespace `kube-ststem`. This service is free of charge, and we recommend you not modify it.
4. Click **OK** and the environment will enter the initialization state. Wait a few minutes, and the environment will be created.

### Step 3. Create a service

1. On the left sidebar, click **Service List** to enter the service list page and select your service deployment region.
2. Click **Create** to access the service creation page and enter the service information.
   ![](https://main.qcloudimg.com/raw/a734a55c6c2c98294fa9da59efc873b5.png)
   - Name: enter a service name.
   - Programming Language: select your programming language.
   - Package Upload Method: select a package upload method. The Java language supports uploading images, JAR packages, and WAR packages, while other languages only support uploading images. If you select **JAR package** or **WAR package**, TEM will automatically build a container image for you and push it to your personal container image repository created by TEM.
3. Click **Next** to enter the deployment service version page. Please configure the relevant parameters according to the specific conditions of your service.
   ![](https://main.qcloudimg.com/raw/0896b68743d26492b7c928f3a5db81ac.png)
   - Upload Package/Image: upload your package or image or download the demos in the console to deploy them and try out all the features of TEM.
   - Release Environment: select the just created environment.
   - Service Port: JAR package demo port number: 8201; WAR package demo port number: 8080; image demo port number: automatically populated.
4. Click **Submit** to complete the creation.

### Step 4. Access the service

TEM provides two ways of access: cross-microservice access and public network access.
- Cross-microservice access: microservices in the same environment can call each other through the registered service names.
- Public network access: click **Edit** on the environment page to view the default domain name and path provided by the system for accessing the services.

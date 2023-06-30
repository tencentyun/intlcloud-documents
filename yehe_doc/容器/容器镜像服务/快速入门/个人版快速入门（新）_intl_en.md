This document describes how to initialize a Tencent Container Registry (TCR) Individual instance, configure a namespace, and push and pull container images.  
To use TCR Enterprise, please see [Quick Start](https://intl.cloud.tencent.com/document/product/1051/35484).


## Step 1: Signing up for a Tencent Cloud Account
If you already have a Tencent Cloud account, ignore this step.
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/account/register" target="_blank"  style="color: white; font-size:13px;">Click here to sign up for a Tencent Cloud account</a></div>

## Step 2: Activating TCR Service

Log in to the [Tencent Cloud console](https://console.cloud.tencent.com/), select **Tencent Cloud services** > **Tencent Container Registry** to enter the TCR console, activate TCR and authorize permissions to it according to the prompts. If you have already authorized permissions to TCR, skip this step.

<div style="background-color:#00A4FF; width: 150px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/tcr/instance?rid=1" target="_blank"  style="color: white; font-size:13px;">Activate TCR</a></div>

## Step 3: Initializing TCR Individual Service
1. Log in to the [TCR console](https://console.cloud.tencent.com/tcr) and go to the “Instance Management” page.
2. Select the region where you want to use the service. Currently, TCR Individual service is only deployed in Guangzhou throughout the Chinese mainland and supports cross-region access through private network in the regions such as Beijing, Shanghai and Chengdu. In this document, we take a TCR Individual instance in Guangzhou region as an example.
3. Check the tab of TCR Individual instance in the region, and click **Initialize Password** to set the password for accessing TCR Individual service. You can reset the password by clicking **More** > **Reset the login password**.
4. After the initialization of the login password is completed, you can click **Log In to Instance** to have the guidance on login of TCR Individual.
    ```
    docker login ccr.ccs.tencentyun.com --username=xxxxxxxxx
    ```
    "username" is the current Tencent Cloud account ID.
    Run this login command in the command line tool, and enter the password. The login is successful if `Login Succeeded` is displayed.

## Step 4: Creating a Namespace
1. Select **Namespace** in the left sidebar. On the "Namespace" page that appears, select "TCR Individual Instance" and click **Create**.
>? Namespaces are used to manage image repositories in the instance. They do not directly store container images, but can map to teams, product projects, or other custom layers in an enterprise.
>
2. In the "Create a Namespace" window, configure the namespace information and click **Confirm**, as shown in the figure below.
   ![](https://main.qcloudimg.com/raw/32391c367d9886afff6a3ccc9df7c458.png)
   - **Name**: it is recommended to use an enterprise team or project name. TCR Individual instance is a shared instance. You cannot create a namespace with the name that has been used by another user.


## Step 6: (Optional) Creating an Image Repository
>? After creating a namespace, you can use the Docker client to push images to the namespace, and the corresponding image repository will be automatically created.
>
1. Click **Image Repository** in the left sidebar to go to the "Image Repository" list page. Select "TCR Individual Instance" at the top of the page.
2. Click **Create**. In the "Create an Image Repository" window, configure the image repository information and click **Confirm**, as shown in the figure below.
In the "Namespace" drop-down list, you can select a created namespace. "Name" cannot be a multi-level path, and "Detailed Description" supports the Markdown syntax.
![](https://main.qcloudimg.com/raw/53e12180c089f48728d4b1cb32552dd2.png)


## Step 7: Pushing and Pulling an Image
After completing the preceding steps, you have created a namespace and image repository. Next, you can perform the following operations to push an image to or pull an image from the image repository.
>? You need to use a CVM or physical machine that has installed the Docker.

### Pushing a container image
You can create a container image on the local server or obtain a public image from Docker Hub for testing.
This document uses the official and latest Nginx image on Docker Hub as an example. In the command line tool, run the following commands sequentially to push this image. Replace `project-a` and `nginx` with the actual namespace and image repository names you have created.
```
sudo docker tag nginx:latest ccr.ccs.tencentyun.com/project-a/nginx:latest
```
```
sudo docker push ccr.ccs.tencentyun.com/project-a/nginx:latest
```

### Pulling a container image
This document uses the successfully pushed Nginx image as an example. In the command line tool, run the following command to pull this image:
```
sudo docker pull ccr.ccs.tencentyun.com/project-a/nginx:latest
```

## What if a problem occurs when I use TCR?
If you encounter a problem while using TCR, locate and solve the problem by referring to the [FAQs](https://intl.cloud.tencent.com/document/product/1051/37243). Alternatively, you can [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category), and we will solve the problem for you as soon as possible.

## Overview
Image Registry is used to store Docker images, which are used to deploy TKE. Each image has a unique ID (image repository address + image name + image tag). Currently, Docker Hub official images and users’ private images are supported.

## Directions
<span id="create"></span>
### Activating Image Registry
>?When using Image Registry for the first time, you need to activate the service.

1. Log in to the TKE console and choose **Image Registry** > **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar.

<span id="openDocker"></span>
2. Complete required information based on the following instructions and click **Enable** to start initialization.
 - **Username**: defaults to the current user’s **Account ID** for logging in to Tencent Cloud Docker Image Registry. You can obtain the username on the [Account Information](https://console.cloud.tencent.com/developer) page.
 - **Password**: is the credential for logging in to Tencent Cloud Docker Image Registry.
 >! Record the username and password, which will be used to push and pull images.

### Creating a namespace
1. Choose **Image Registry** > **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar to go to the "My Images" page.
2. On the "My Images" page, select the **Namespace** tab and click **Create**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/399d9b928672a49d8fa8d271e52a74cd.png)
3. In the "Create a Namespace" window that appears, enter the namespace name and click **Submit**, as shown in the figure below:
>?
>- The namespace name must be unique in the region to which the namespace belongs. If the namespace name that you want to use is already used by another user, try another name.
>- At the top of the **My Images** page, select a region from the list.

![](https://main.qcloudimg.com/raw/32391c367d9886afff6a3ccc9df7c458.png)


### Creating an image
1. Choose **Image Registry** > **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar to go to the "My Images" page.
2. On the "My Images" page, click **Create** above the image list, as shown in the figure below:
![](https://main.qcloudimg.com/raw/83f0f563e27161b21d59cba2bc9ebdd5.png)
3. Enter the image name and description, and then click **Submit**.
>? The namespace is used to classify container images. It is also the prefix of the addresses of private images that you create. This document uses `tkefiletest` as an example.

![](https://main.qcloudimg.com/raw/53e12180c089f48728d4b1cb32552dd2.png)

### Pushing an image to Image Registry
>? Image addresses vary slightly with different regions. In the following steps, the image address of the default region is used as an example. In real-world cases, replace the image address with the correct one. You can query the actual image address on the [My Images](https://console.cloud.tencent.com/tke2/registry/user/self?rid=1) page.

#### Logging in to Tencent Cloud Registry
1. On a client, replace the variable in the following command with the actual one and run the command to log in to Tencent Cloud Registry.
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
**username**: refers to Tencent Cloud **Account ID**, which is registered upon service activation. You can obtain the username on the [Account Information](https://console.cloud.tencent.com/developer) page.
2. Enter the password that you set when [activating image registry](#create) to complete login. 

#### Uploading an image
Replace the variables in the following commands and run them to upload the image.
```
$ sudo docker tag [ImageId] ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image tag]
$ sudo docker push ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image tag]
```
- **ImageId and Image tag**: enter them based on existing image information.
- **namespace**: indicates the namespace that you entered when activating Image Repository.
- **ImageName**: indicates the image name created in the console.


#### Downloading an image
1. Run the following command to log in to Image Repository. In this step, you need to enter the password that you set when [activating Image Registry](#create).
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
2. Replace the variable in the following command and run the command to download the image.
```
$ sudo docker pull ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image tag]
```

### Deleting an image
1. Choose **Image Registry** > **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar to go to the "My Images" page.
2. On the "My Images" page, click **Delete** for the target image.
3. In the "Delete Image Repository" window that appears, click **OK** to **delete all tags of the image**, as shown in the figure below:
![](https://main.qcloudimg.com/raw/f44b2b1cf102bea6da97d11f85718f97.png)

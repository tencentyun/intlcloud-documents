## Overview
Image Registry is used to store Docker images, which are used to deploy Tencent Kubernetes Engine (TKE). Each image has a unique ID (image repository address + image name + image tag). Currently, Docker Hub official images and users' private images are supported.

## Directions

<span id="create"></span>

## Activating Image Registry

>?Users who use Image Registry for the first time need to activate the service first.
>
1. Log in to the TKE console, and choose **Image Registry** > **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar.
2. <span id="openDocker"></span>Enter relevant information according to the following instructions and click **Enable** to start initialization, as shown in the figure below.
![](https://main.qcloudimg.com/raw/1edfed553fce284d1f66e356494ae78c.png)
 - **Username**: by default, this parameter is set to the current user's **Account ID**, namely the identity with which you log in to Tencent Cloud Docker Image Registry. It can be obtained on the [Account Information](https://console.cloud.tencent.com/developer) page.
 - **Password**: this is the credential you use to log in to Tencent Cloud Docker Image Registry.
 >!Take note of the user name and password, which will be used to push and pull images.

### Creating a namespace
1. Choose **Image Registry** > **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar to go to the "My Images" page.
2. On the "My Images" page, select the **Namespace** tab and click **Create**, as shown in the figure below.
![](https://main.qcloudimg.com/raw/399d9b928672a49d8fa8d271e52a74cd.png)
3. In the **Create Namespace** window that appears, enter the namespace name and click **Submit**, as shown in the figure below.
>?
>- The namespace name must be unique in the region to which the namespace belongs. If the namespace name you want to use is already in use by another user, try another available name.
>- Select a region from the list at the top of the "My Images" page.
>
![](https://main.qcloudimg.com/raw/32391c367d9886afff6a3ccc9df7c458.png)


### Creating an image
1. Select **Image Repository** > **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar to go to the **My Images** page.
2. On the "My Images" page, click **Create** above the image list, as shown in the figure below.
![](https://main.qcloudimg.com/raw/83f0f563e27161b21d59cba2bc9ebdd5.png)
3. Enter the image name and description, and click **Submit**.
>?The namespace is used to classify container images. It is also the prefix of the address of the private images that you create. This document uses `tkefiletest` as an example.
>
![](https://main.qcloudimg.com/raw/53e12180c089f48728d4b1cb32552dd2.png)

### Pushing an image to image registry
>? The image address varies depending on the region. In the following steps, the image address in the default region is used as an example. Replace it with the correct image address during actual operations. You can view the image address in [My Images](https://console.cloud.tencent.com/tke2/registry/user/self?rid=1).
>
#### Logging in to Tencent Cloud Registry
1. On the terminal, replace relevant information in the following command and run it to log in to Tencent Cloud Registry.
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
**username**: Tencent Cloud **Account ID**, registered upon service activation. You can obtain it on the [Account Information](https://console.cloud.tencent.com/developer) page.
2. Enter the password that you set when [activating Image Registry](#create) to complete login.
>? When you use `sudo` command to execute docker login, the system will prompt you to enter the host admin password required by sudo first. After correctly entering it and confirming no errors, you enter the correct image registry login password again and login successfully.


#### Uploading an image
Replace the relevant information in the following commands and then run them to upload an image.
```
$ sudo docker tag [ImageId] ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image Tag]
$ sudo docker push ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image Tag]
```
- **ImageId**: ID of the image to be uploaded, which can be viewed by running `docker image ls`.
- **Image Tag**: image tag of an image uploaded to Image Registry.
- **namespace**: the namespace you entered when activating Image Registry.
- **ImageName**: the image name created in the console.


#### Downloading an image
1. Run the following command to log in to Image Registry. You need to enter the password set when [activating Image Registry](#create).
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
2. Replace the relevant information in the following command and run it to download the image.
```
$ sudo docker pull ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image Tag]
```

### Deleting an image
1. Select **Image Repository** > **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar to go to the **My Images** page.
2. On the "My Images" page, click **Delete** on the right of the row where the image to be deleted is located.
3. In the **Delete Image Repository** window that appears, click **OK** to **delete all tags of the image**, as shown in the figure below.
![](https://main.qcloudimg.com/raw/f44b2b1cf102bea6da97d11f85718f97.png)


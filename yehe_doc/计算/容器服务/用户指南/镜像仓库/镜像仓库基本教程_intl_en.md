## Scenario
Image Registry is used to store Docker images, which are used to deploy TKE. Each image has a unique ID (image repository address + image name + image tag). Currently, Docker Hub official images and users’ private images are supported.

## Directions

### Activating Image Registry<span id="create"></span>
>Users who use Image Registry for the first time need to activate the service first.
>
1. Log in to the TKE Console, and select **Image Registry** -> **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar.
2. <span id="openDocker"></span>Enter relevant information according to the following instructions and click **Enable** to start initialization.

 - **User name**: by default, this parameter is the current user’s **Account ID**, namely the identity with which you log in to Tencent Cloud Docker Image Registry. It can be obtained on the [Account Information](https://console.cloud.tencent.com/developer) page.
 - **Password**: this is the credential you use to log in to Tencent Cloud Docker Image Registry.
 >Take note of the user name and password, which will be used to push and pull images.

### Creating a namespace
1. Select **Image Registry** -> **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar to go to the **My Images** page.
2. On the **My Images** page, choose the **Namespace** tab and click **Create**.

3. In the **Create a Namespace** window that pops up, enter the namespace name and click **Submit**, as shown in the following figure:
>
>- The namespace name must be unique in the region to which the namespace belongs. If the namespace name you want to use is already in use by another user, try an available name.
>- Select a region from the list at the top of the **My Images** page.
>


### Creating an image
1. Select **Image Registry** -> **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar to go to the **My Images** page.
2. On the **My Images** page, click **Create** above the image list.
3. Enter the image name and description, and then click **Submit**.
>The namespace is used to classify container images. It is also the prefix of the address of the private images that you create. This document uses `tkefiletest` as an example.
>

### Pushing an image to Image Registry
#### Logging in to Tencent Cloud Registry
1. On the terminal, replace relevant information in the following command and run it to log in to Tencent Cloud Registry.
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
**username**: Tencent Cloud **Account ID**, registered upon service activation. You can obtain it on the [Account Information](https://console.cloud.tencent.com/developer) page.
2. Enter the password that you set when [activating Image Registry](#create) to complete login. 

#### Uploading image
Replace the relevant information in the following commands and then run them to upload the image.
```
$ sudo docker tag [ImageId] ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image Tag]
$ sudo docker push ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image Tag]
```
- **ImageId and image tag**: enter based on existing image information.
- **namespace**: the namespace you entered when activating Image Repository.
- **ImageName**: the image name created in the console.


#### Downloading image
1. Run the following command to log in to Image Repository. You need to enter the password set when [activating Image Registry](#create).
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
2. Replace the relevant information in the following command and run it to download the image.
```
$ sudo docker pull ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image Tag]
```

### Deleting an image
1. Select **Image Registry** -> **[My Images](https://console.cloud.tencent.com/tke2/registry/user/self)** in the left sidebar to go to the **My Images** page.
2. On the **My Images** page, click **Delete** to the right of the row where the image to be deleted is located.
3. In the **Delete Image Repository** window that pops up, click **OK** to **delete all tags of the image**.


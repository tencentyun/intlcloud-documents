## Image Registry Overview
The image registry is used to store Docker Hub images, which are used to deploy TKE. Each image has a unique ID (image registry address + image name + image tag).

## Image Type
Currently, Docker Hub images and users’ private images are supported.

## Activating Image Registry
![Alt text](https://mc.qcloudimg.com/static/img/b0ce4b921b60f4f79fec6be455e16f4f/Image+005.png)
Users who use image registry for the first time need to activate this service first.

- **Namespace**: This is the prefix for the addresses of private images you create.
- **Username**: By default, this is the account of the current user. Use this account to log in to Tencent Cloud Docker Hub Image Registry.
- **Password**: This is the credential to log in to Tencent Cloud Docker Hub Image Registry.

## Creating Image
1. Click **Create** on the image list page.
![Alt text](https://mc.qcloudimg.com/static/img/73e7951509c8bef8f7eaf703af6cb8df/Image+001.png)
2. Enter the image name and description, and then click **Submit**.
![Alt text](https://mc.qcloudimg.com/static/img/026b93deb76bfaeff5a27d24878529a2/Image+003.png)

## Pushing Image to Image Registry
### Logging in to Tencent Cloud Registry
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
username: The Tencent Cloud account you registered. Enter your password to login.
### Uploading Image
```
$ sudo docker tag [ImageId] ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image Tag]
$ sudo docker push ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image Tag]
```
- `ImageId` and image tag should be entered according to the image details.
- `namespace` is the namespace you entered when activating your image registry.
- `ImageName` is the image name created on the console.


## Downloading Image
Enter the password and log in to image registry.
```
$ sudo docker login --username=[username] ccr.ccs.tencentyun.com
```
Download the image.
```
$ sudo docker pull ccr.ccs.tencentyun.com/[namespace]/[ImageName]:[Image Tag]
```

## Deleting Image
Select the image, click **Delete** and then click **OK**. All tags of the image will be deleted.
![Alt text](https://mc.qcloudimg.com/static/img/7bc3adadf35e8d452a380c613abb264e/Image+050.png)

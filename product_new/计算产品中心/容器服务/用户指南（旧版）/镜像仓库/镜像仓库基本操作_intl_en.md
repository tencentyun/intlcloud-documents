## Image Registry Overview
The image registry is used to store Docker Hub images, which are used to deploy TKE. Each image has a unique ID (image registry address + image name + image tag).

## Image Type
Currently, Docker Hub images and users’ private images are supported.

## Activating Image Registry
![Alt text](https://main.qcloudimg.com/raw/19b5216380d339b0b6b2d7742f847cbf.png)
Users who use image registry for the first time need to activate this service first.

- **Namespace**: This is the prefix for the addresses of private images you create.
- **Username**: By default, this is the account of the current user. Use this account to log in to Tencent Cloud Docker Hub Image Registry.
- **Password**: This is the credential to log in to Tencent Cloud Docker Hub Image Registry.

## Creating Image
1. Click **Create** on the image list page.
![Alt text](https://main.qcloudimg.com/raw/2c704951542f736e21ce0d5cec1c178c.png)
2. Enter the image name and description, and then click **Submit**.
![Alt text](https://main.qcloudimg.com/raw/c10278379a87f962c24c42abb83746ca.png)

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
![Alt text](https://main.qcloudimg.com/raw/cb73a61a4aa649373b2bcaa41af38143.png)

## Operation Scenarios
This document describes how to complete auto-building of Github-based images by in TKE console. 

## Prerequisites
- You are logged in to the [TKE Console](https://console.cloud.tencent.com/tke2).
- You’ve obtained the access to the source code. 

## Directions
1. Select **Image Repository** > **[My Images](https://console.cloud.tencent.com/tke2/registry/user)** in the left sidebar to go to the **My Images** page.
2. On the **My Images** page, click **Build Configuration** to the right of the row where the image is located. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/7ceff861b8e66a1f025fdacc89908a1b.png)
3. Go to the building rule page, and refer to the following steps to configure the related information.

### Building configurations for Github-based images
Configure Github build rules according to the following information, and click **Complete**. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/843bd3a5889ec6d601224973631bb567.png)

 - **Code source**: select **Github**.
 - **Organization**: select your organization (usually your Github account), or choose one of the organizations you belong to.
 - **Repository**: select a registry through which you need to build a container image.
 - **Triggering method**: specifies a condition to build a container image automatically when the code is pushed to a branch or a new Tag. You can also leave it blank and build an image manually on the image building page.
 - **Version naming rule**: the container image **Tag naming rule**. An image tag can be formatted.
  - **Branch/tag**: it can contain branch name/repository Tag name.
  - **Update time**: the time when the image is built
  - **commit number**: the latest commit number of the branch/Tag.
 > If an image is automatically built based on a branch or a Tag, and the naming rule contains branch/Tag, the branch or Tag name should be a combination of uppercase/lowercase letters, underscores (`_`), and dashes (`-`), and cannot contain special characters as `/`, `$`, etc.
 >
 - **Overwrite the image tag**: after building, an image with the same tag name will be generated, and will overwrite the existing image with the same name.
 - **Dockerfile path**: The **Relative Path** of Dockerfile in the registry. It is left empty by default. If it is not specified, Dockerfile is located in the project's root directory. The file name must be "Dockerfile" starting with a capital D. If Dockerfile is located in another directory (e.g. the build directory in the registry) and the file name is Dockerfile, the Dockerfile path is: `build/Dockerfile`.
 - **Building directory**: the working directory for the build. Dockerfile commands will be executed in this directory.
 - **Building parameters**: the parameters that are passed in when the image is built. These can be used to set environment variables.


### Building Gitlab-based images
Complete configurations for building Gitlab-based images as instructed below:
![](https://main.qcloudimg.com/raw/5dd910649ef3fee0b10d93800a9f2985.png)
- **Code source**: select **Gitlab**.
- **Group**: select a Gitlab Group.
- **Repository**: select a registry through which you need to build a container image.
- **Triggering method**: supports multiple choices. The building of a container image can be automatically triggered when the code is pushed to a branch or a new Tag. You can leave it blank and build an image manually on the image building page.
- **Version naming rule**: the container image **Tag naming rule**. An image tag can be formatted.
 - **Branch/tag**: can contain branch/repository Tag name.
 - **Update time**: the time when the image is built
 - **commit number**: the latest commit number of the branch/Tag.
 > If an image is automatically built based on a branch or a Tag, and the naming rule contains branch/Tag, the branch or Tag name should be a combination of uppercase/lowercase letters, underscores (`_`), and dashes (`-`), and cannot contain special characters as `/`, `$`, etc.
 >
- **Overwrite the image tag**: after building, an image with the same tag name will be generated, and will overwrite the existing image of the same name.
- **Dockerfile path**: The **Relative Path** of Dockerfile in the registry. It is left empty by default. If it is not specified, Dockerfile is located in the project's root directory. The file name must be "Dockerfile" starting with a capital “D”. If Dockerfile is located in another directory (e.g. the build directory in the registry) and the file name is Dockerfile, the Dockerfile path is: `build/Dockerfile`.
- **Building directory**: the working directory for the build. Dockerfile commands will be executed in this directory.
- **Building parameters**: the parameters that are passed in when the image is built. These can be used to set environment variables.


### Auto building
Select a triggering method in the configuration, and a container image is automatically built when you submit a new branch or push the code to the specified registry. The entire building process is implemented on the Tencent Cloud TKE platform. After you finish building, a new image is generated according to the version naming rule you defined, and uploaded to the Tencent Cloud TKE image registry.


## FAQs
For more information on the source code build Dockerfile file path issue, see [Image Build FAQs](https://intl.cloud.tencent.com/document/product/457/6785).



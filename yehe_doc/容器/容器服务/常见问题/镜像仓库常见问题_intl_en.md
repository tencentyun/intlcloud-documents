## Image Registry Activation FAQs

### What is a namespace used for?

A namespace is an address prefix that identifies a user’s private images.

### What is an Image Registry account?

By default, this account is your Tencent Cloud account (QQ number).

### What should I do if I forget the password set during activation?

You can reset the password in the console.

## Cluster Creation FAQs

### Is there a quota limit on the number of created images?

Yes. The default quota is 500 image repositories per region and 100 image tags per image repository.
If you need a higher quota, [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=350&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E5%AE%B9%E5%99%A8%E6%9C%8D%E5%8A%A1CCS).

### Can I share my created images with other users?

No, this feature is currently not supported.

### How do I use the created images?

First, upload available image tags and then create services by using specific image tags.

## Image Deletion FAQs

### How do I delete a certain tag of an image?

You can specify and delete a certain tag directly from the console.

### When I delete an image from the image list, will all tags of the image be deleted too?

Yes. Be sure to back up your data in advance.

## Image Building FAQs

### How do I specify the Dockerfile path and building directory when building an image by using source code?
- If you do not enter a path, the system uses the following default values:
 - Default Dockerfile path: Dockerfile under the root directory of the repository (`Dockerfile`).
 - Default building directory: root directory of the repository (`./`).
- To specify a path, **enter a relative path with the project path as the root path**, as shown in the following figure:
![](https://main.qcloudimg.com/raw/438df3f167953435eb06363859c7b25a.png)

### How does the source code building feature use the Dockerfile path and building directory?
To implement the feature of building images with source code, you need to first clone the user-specified repository, then switch to the corresponding branch or tag, and lastly run the command `docker build -f $DOCKERFILE_PATH $WORKDIR` in the root directory of the code repository to build a container image.

### How do I specify the source path in Dockerfile?
For `COPY`, `ADD`, and other commands related to the source path, specify the source path as a path relative to the building directory.

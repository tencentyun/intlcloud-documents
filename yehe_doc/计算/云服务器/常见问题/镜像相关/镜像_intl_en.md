### What is an image?

An image is the template for CVM software configuration (operating systems, pre-installed programs, etc.). Tencent Cloud requires users to launch the instance using an image. An image can launch multiple instances, so users can use it repeatedly. For more information on images, please see [Overview](https://intl.cloud.tencent.com/document/product/213/4940).

### What should I prepare before importing an image?

Before importing an image, you need to complete two major steps: applying for permissions and preparing image files. For more information, please see [Overview](https://intl.cloud.tencent.com/document/product/213/4945).

### What should I do if the Windows system fails to create a custom image?

If the Windows system fails to create a custom image, check by following the steps below:
1. The creation of a custom image relies on the Windows Modules Installer provided by Microsoft. Make sure this service is working properly.
2. Some antivirus tools or Safedog may block custom image creation scripts from executing. To avoid creation failure, we recommend you close these tools before creating a custom image.
3. If the image creation tool is interrupted by system pop-ups, remotely log in to the CVM, then check and adjust the CVM configuration to avoid pop-ups.

### How many users can each image be shared to at the most?

50 users.

### Can the name and description of a shared image be changed?

No.

### Does a shared image count toward my image quota?

No.

### Are there any region limitations on the shared image for creating and reinstalling a CVM instance?

Yes. The shared image should be in the same region as the source image. The CVM instance can only be created and reinstalled in the same region.

### Can a shared image be copied to other regions?

No.

### Can a custom image that has been shared to other users be deleted?

Yes, but you need to cancel all sharing for this custom image first.

### Can an image shared by other users be deleted?

No.

### What are the risks of using custom images shared by other users?

Tencent Cloud does not guarantee the integrity and security of images shared by other users. Please select images shared by a trusted account.

### Can I share with others an image another user shared with me?

No.

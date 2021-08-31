### What is the maximum number of users an image can be shared with?

50 users.

### Can the name and description of a shared image be changed?

No.

### Does a shared image count toward my image quota?

No.

### Are there any region limitations for a shared image on creating and reinstalling a CVM instance?

Yes. The shared image should be in the same region as the source image. The CVM instance can only be created and reinstalled in the same region.

### Can a shared image be copied to other regions?

No.

### Can a custom image that has been shared with other users be deleted?

Yes, but you need to cancel all sharing for this custom image first.

### Can an image shared by other users be deleted?

No.

### What are the risks of using a custom image shared by other users?

Tencent Cloud does not guarantee the integrity and security of images shared by other users. Please select images shared by a trusted account.

### Can I share with others an image another user shared with me?

No.

### What are the risks of sharing a custom image with another account?

Data and software leakage may occur. Before sharing a custom image with another account, make sure the image has no sensitive data or software. Be aware that the account you share the image with can create CVM instances from the shared image to create more custom images. The constant transfer of data will increase the risk of leakage.

### Can I create an instance using an image that I shared with other users?

Yes. You can create a CVM instance using the image you shared with another account. You can also create a custom image based on the CVM instance.

### Can an image created on Server A in North China be shared with Server B in East China?

- If both servers are under the same account, you can directly copy the image to Server B in East China. For detailed directions, see [Copying Images](https://intl.cloud.tencent.com/document/product/213/4943)
- If both servers are under different accounts, you need to copy the image to the East China region and then share it with the account of Server B. For detailed directions, see [Copying Images](https://intl.cloud.tencent.com/document/product/213/4943), [Sharing Custom Images](https://intl.cloud.tencent.com/document/product/213/4944), and [Cancelling Image Sharing](https://intl.cloud.tencent.com/document/product/213/7148).

